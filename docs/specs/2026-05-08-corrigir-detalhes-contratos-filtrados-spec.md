---
date: 2026-05-08T10:16:50-03:00
author: Codex
status: draft
ticket: null
research: /Users/lucasruon/Downloads/docs/research/2026-05-08-rota-contratos-ver-detalhes.md
---

# Spec: Corrigir Detalhes de Contratos Filtrados

**Data**: 2026-05-08
**Estimativa**: Pequena

## Objetivo

Corrigir a tela de contratos para que o botão "Ver Detalhes", "Conferir e Aprovar", "Aprovar Revisão" e "Solicitar Revisão" sempre abra e envie ações para o contrato correto, inclusive quando o filtro mensal estiver ativo.

Hoje a tela renderiza os cards a partir de um array filtrado, mas passa para o modal o índice desse array filtrado. O modal interpreta esse mesmo índice como posição dentro de `allContratos`, que é o array completo retornado por `get-contratos`. Com isso, ao filtrar, o card de um cliente pode abrir os detalhes de outro contrato.

## Escopo

### Incluído

- Ajustar a referência usada pelos cards de contrato para apontar para a posição original em `allContratos`.
- Garantir que `abrirModalContrato()`, `confirmarAprovacao()` e `confirmarRevisao()` continuem usando o contrato correto depois do filtro.
- Manter o filtro mensal aplicado após aprovar contrato ou solicitar revisão.
- Adicionar verificações manuais objetivas para o cenário Carmem/Tadeu descrito na pesquisa.

### Não Incluído

- Alterar os webhooks do n8n (`get-contratos`, `aprovar-contrato`, `solicitar-revisao`).
- Criar uma rota backend individual para detalhes do contrato.
- Refatorar a aplicação para separar HTML, CSS e JavaScript em arquivos distintos.
- Alterar layout, status do kanban ou regras de negócio de aprovação/revisão.

## Pré-requisitos

- [ ] Ter acesso ao arquivo `/Users/lucasruon/Downloads/sava-novos-negocios.html`.
- [ ] Ter pelo menos dois contratos no retorno de `get-contratos`, preferencialmente em meses/ordens que reproduzam a divergência de índice.
- [ ] Confirmar que o filtro de mês `filtroMesContrato` está sendo usado na tela de contratos.

## Fases de Implementação

### Fase 1: Preservar o Índice Original do Contrato

**Objetivo:** Fazer cada card renderizado carregar a posição correta do contrato dentro de `allContratos`, mesmo quando `renderContratos()` recebe um array filtrado.

#### Arquivos a Modificar

| Arquivo | Ação | Descrição |
|---------|------|-----------|
| `sava-novos-negocios.html` | Modificar | Ajustar `renderContratos()` para usar o índice original em `allContratos` em vez do índice local do array filtrado. |

#### Detalhes de Implementação

1. `sava-novos-negocios.html`
   - Localizar `function renderContratos(contratos)`.
   - Trocar a criação do agrupamento atual:

```javascript
contratos.forEach(function (c, idx) {
    var s = c.status || 'aguardando_aprovacao';
    if (!grouped[s]) grouped[s] = [];
    grouped[s].push({ contrato: c, index: idx });
});
```

   - Por uma versão que calcula a posição do mesmo objeto em `allContratos`:

```javascript
contratos.forEach(function (c) {
    var s = c.status || 'aguardando_aprovacao';
    var originalIndex = allContratos.indexOf(c);
    if (originalIndex === -1) return;
    if (!grouped[s]) grouped[s] = [];
    grouped[s].push({ contrato: c, index: originalIndex });
});
```

   - Manter os botões existentes chamando `abrirModalContrato(idx, ...)`, mas agora `idx` deve ser o índice original em `allContratos`.
   - Não alterar o contrato de `abrirModalContrato(index, abrirRevisao)` nesta fase para reduzir risco, já que `confirmarAprovacao()` e `confirmarRevisao()` dependem de `currentContratoIndex`.

#### Critérios de Sucesso

**Verificação Automatizada:**
- [x] Executar `rg -n "grouped\\[s\\]\\.push\\(\\{ contrato: c, index: idx \\}\\)|allContratos\\.indexOf\\(c\\)" sava-novos-negocios.html` e confirmar que não existe mais `index: idx` no agrupamento de contratos e existe `allContratos.indexOf(c)`.

**Verificação Manual:**
- [ ] Abrir a tela de contratos com filtro mensal ativo.
- [ ] Clicar em "Ver Detalhes" em um contrato filtrado da Carmem.
- [ ] Confirmar que o modal mostra nome, área, tipo, advogado, data, histórico e link do Drive da Carmem, não de Tadeu.
- [ ] Repetir em pelo menos um contrato de outra coluna do kanban.

### Fase 2: Manter o Filtro Depois de Aprovar ou Solicitar Revisão

**Objetivo:** Evitar que ações feitas dentro do modal removam visualmente o filtro mensal ativo e reduzam a chance de confusão operacional.

#### Arquivos a Modificar

| Arquivo | Ação | Descrição |
|---------|------|-----------|
| `sava-novos-negocios.html` | Modificar | Substituir rerenderizações diretas por `filtrarContratosPorMes()` depois de atualizar status local. |

#### Detalhes de Implementação

1. `sava-novos-negocios.html`
   - Em `confirmarAprovacao()`, após sucesso, manter a atualização:

```javascript
allContratos[currentContratoIndex].status = 'em_assinatura';
```

   - Substituir:

```javascript
renderContratos(allContratos);
atualizarStatsContratos(allContratos);
```

   - Por:

```javascript
filtrarContratosPorMes();
```

   - Em `confirmarRevisao()`, após sucesso, manter a atualização:

```javascript
allContratos[currentContratoIndex].status = 'revisao_solicitada';
```

   - Substituir o mesmo par `renderContratos(allContratos)` e `atualizarStatsContratos(allContratos)` por `filtrarContratosPorMes()`.
   - Validar que `filtrarContratosPorMes()` já cuida de `renderContratos()` e `atualizarStatsContratos()` tanto com mês selecionado quanto sem filtro.

#### Critérios de Sucesso

**Verificação Automatizada:**
- [x] Executar `rg -n "allContratos\\[currentContratoIndex\\]\\.status|renderContratos\\(allContratos\\)|filtrarContratosPorMes\\(\\)" sava-novos-negocios.html` e confirmar que, dentro dos blocos de sucesso de aprovação/revisão, há chamada a `filtrarContratosPorMes()` e não há rerender direto com `allContratos`.

**Verificação Manual:**
- [ ] Selecionar um mês no filtro.
- [ ] Abrir um contrato filtrado em "Conferir e Aprovar" ou "Solicitar Revisão".
- [ ] Concluir a ação com sucesso.
- [ ] Confirmar que a tela continua exibindo o mês selecionado e que os cards/contadores refletem o status atualizado dentro desse filtro.

### Fase 3: Validar Fluxos com e sem Filtro

**Objetivo:** Confirmar que a correção resolve o bug original e não quebra o comportamento existente sem filtro.

#### Arquivos a Modificar

| Arquivo | Ação | Descrição |
|---------|------|-----------|
| `sava-novos-negocios.html` | Modificar | Apenas ajustes finos se algum fluxo manual revelar inconsistência. |

#### Detalhes de Implementação

1. `sava-novos-negocios.html`
   - Testar a tela sem filtro, com filtro mensal ativo e após recarregar a lista via navegação para `screenContratos`.
   - Verificar que `currentContratoIndex` sempre aponta para uma posição válida em `allContratos`.
   - Confirmar que `closeContratoModal()` continua limpando `currentContratoIndex = null`.
   - Se houver casos em que `allContratos.indexOf(c)` retorne `-1`, adicionar uma função auxiliar próxima de `renderContratos()` para resolver por `id` como fallback:

```javascript
function getContratoOriginalIndex(contrato) {
    var index = allContratos.indexOf(contrato);
    if (index !== -1) return index;
    if (!contrato || !contrato.id) return -1;
    return allContratos.findIndex(function (item) {
        return item && item.id === contrato.id;
    });
}
```

   - Usar esse fallback apenas se os dados forem clonados antes de chegar em `renderContratos()`. No fluxo atual, `filtered` preserva a referência dos objetos de `allContratos`, então `indexOf(c)` deve ser suficiente.

#### Critérios de Sucesso

**Verificação Automatizada:**
- [x] Executar `node --check sava-novos-negocios.html` somente se o JavaScript for extraído ou validado por ferramenta compatível; caso contrário, pular e registrar que o arquivo HTML inline não é diretamente validável por `node --check`. Validado por extração do `<script>` inline e compilação com `new Function(...)`.
- [x] Executar `rg -n "abrirModalContrato\\(|currentContratoIndex|allContratos\\[currentContratoIndex\\]" sava-novos-negocios.html` para revisar manualmente todos os pontos que dependem do índice.

**Verificação Manual:**
- [ ] Sem filtro de mês, abrir "Ver Detalhes" em três contratos de posições diferentes e confirmar dados corretos.
- [ ] Com filtro de mês, abrir "Ver Detalhes" em três contratos de posições diferentes e confirmar dados corretos.
- [ ] Com filtro de mês, acionar "Solicitar Revisão" e confirmar que o payload enviado usa `contrato_id`, `cliente_nome` e `advogado_nome` do contrato exibido no modal.
- [ ] Com filtro de mês, acionar "Conferir e Aprovar" e confirmar que o payload enviado usa `contrato_id`, `cliente_nome`, `cliente_email` e `link_drive` do contrato exibido no modal.

## Edge Cases

| Cenário | Comportamento Esperado |
|---------|------------------------|
| Filtro mensal ativo e primeiro card filtrado corresponde ao índice 7 de `allContratos` | O botão deve chamar `abrirModalContrato(7, ...)` e o modal deve mostrar o contrato correto. |
| Contrato filtrado não existe mais em `allContratos` | O card deve ser ignorado ou o modal não deve abrir, sem mostrar dados de outro contrato. |
| Contrato sem `id` retornado pelo webhook | A correção deve continuar funcionando por referência de objeto e índice original. |
| Contrato sem `data_geracao` | Deve continuar fora do filtro mensal, como ocorre hoje. |
| Nenhum mês selecionado | A listagem deve continuar usando `allContratos`, mantendo o comportamento atual. |
| Aprovação/revisão com filtro ativo | O status local deve mudar e a tela deve continuar filtrada pelo mês selecionado. |
| Fechar modal sem ação | `currentContratoIndex` deve voltar para `null` e nenhuma ação deve ser enviada. |

## Riscos e Mitigações

- Uso de `indexOf(c)` depende de `filtered` preservar referência dos objetos de `allContratos` -> O fluxo atual usa `allContratos.filter(...)`, que preserva referência; se isso mudar, aplicar o fallback por `id` descrito na Fase 3.
- Mutação local de status pode deixar a lista temporariamente diferente do backend se o webhook demorar a refletir a mudança -> Manter comportamento atual e, se necessário em trabalho futuro, chamar `carregarContratos()` após sucesso para reconciliar com backend.
- Botões inline com `onclick` continuam acoplados a índice numérico -> Manter por enquanto para correção pequena; uma refatoração futura pode trocar para `data-contrato-id` e event delegation.
- Dados sensíveis de contratos são enviados para aprovação/revisão -> Não adicionar novos campos ao payload; preservar somente os campos já enviados atualmente.

## Rollback

1. Reverter as alterações em `renderContratos()` para voltar a usar o índice local `idx`.
2. Reverter as chamadas pós-sucesso de `filtrarContratosPorMes()` para `renderContratos(allContratos)` e `atualizarStatsContratos(allContratos)`.
3. Reexecutar o teste manual sem filtro para confirmar que o comportamento anterior foi restaurado.
4. Nenhum rollback de dados é necessário, pois a mudança é somente front-end.

## Checklist Final

- [x] Scope implemented
- [ ] Validation complete
- [ ] Rollback path verified
