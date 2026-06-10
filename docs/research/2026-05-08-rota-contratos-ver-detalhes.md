---
date: 2026-05-08T10:13:35-03:00
researcher: Codex
git_commit: n/a
branch: n/a
repository: Downloads
topic: "$research-codebase '/Users/lucasruon/Downloads/sava-novos-negocios.html' verifique a rota dos contratos, no botão \"Ver detalhes\" porque mesmo quando eu adiciono um contrato novo e clico nesse botão, o popup com os detalhes está trazendo informações incorretas. Um exemplo, tive um contrato da Carmem, mas quando eu abro, está trazendo informações do contrado do Tadeu"
tags: [research, codebase]
status: complete
last_updated: 2026-05-08
last_updated_by: Codex
---

# Research: Rota dos contratos no botão "Ver Detalhes"

**Date**: 2026-05-08T10:13:35-03:00
**Researcher**: Codex
**Git Commit**: n/a
**Branch**: n/a
**Repository**: Downloads

## Research Question

$research-codebase '/Users/lucasruon/Downloads/sava-novos-negocios.html' verifique a rota dos contratos, no botão "Ver detalhes" porque mesmo quando eu adiciono um contrato novo e clico nesse botão, o popup com os detalhes está trazendo informações incorretas. Um exemplo, tive um contrato da Carmem, mas quando eu abro, está trazendo informações do contrado do Tadeu

## Scope

Pesquisa focada no arquivo `/Users/lucasruon/Downloads/sava-novos-negocios.html`, especialmente no envio de novos negócios, carregamento de contratos, renderização dos cards e abertura do modal de detalhes. Não foi inspecionado o workflow/backend externo do n8n e nenhuma chamada HTTP externa foi executada.

## Summary

A tela de contratos não possui uma rota individual para buscar detalhes de um contrato ao clicar em "Ver Detalhes". Ela carrega todos os contratos uma vez via `get-contratos`, guarda a resposta em `allContratos`, renderiza os cards e depois abre o modal usando um índice numérico.

O comportamento observado tem correspondência direta no código: quando há filtro de mês ativo, `filtrarContratosPorMes()` cria um array `filtered` e chama `renderContratos(filtered)`. Dentro de `renderContratos`, o botão "Ver Detalhes" recebe o índice desse array filtrado. Porém `abrirModalContrato(index, ...)` usa esse índice para acessar `allContratos[index]`, que é o array completo. Assim, o card exibido para Carmem pode enviar `0`, mas o modal lê `allContratos[0]`, que pode ser Tadeu.

## Detailed Findings

### Rotas Envolvidas

- As URLs da aplicação ficam em `API_URLS` no próprio HTML (`sava-novos-negocios.html:3781`).
- Novo negócio/contrato é enviado por `novosNegocios`, com URL `https://n8n-n8n.zfp6fw.easypanel.host/webhook/novos-negocios` (`sava-novos-negocios.html:3784`).
- A listagem de contratos usa `getContratos`, com URL `https://n8n-n8n.zfp6fw.easypanel.host/webhook/get-contratos` (`sava-novos-negocios.html:3790`).
- Aprovação e revisão usam `aprovarContrato` e `solicitarRevisao` (`sava-novos-negocios.html:3791`, `sava-novos-negocios.html:3792`).

### Envio de Novo Negócio

- O formulário `novosNegociosForm` monta um objeto `data` com dados do cliente, negócio, honorários, negociação e abertura de pasta (`sava-novos-negocios.html:4372`, `sava-novos-negocios.html:4385`).
- O envio é feito com `fetch(API_URLS.novosNegocios, { method: 'POST', ... })` (`sava-novos-negocios.html:4436`).
- Após sucesso, o formulário é resetado e a tela rola para o topo (`sava-novos-negocios.html:4440`, `sava-novos-negocios.html:4441`, `sava-novos-negocios.html:4451`).

### Carregamento da Tela de Contratos

- Ao navegar para `screenContratos`, a função `navigateTo()` chama `carregarContratos()` (`sava-novos-negocios.html:3902`, `sava-novos-negocios.html:3912`).
- `carregarContratos()` faz `fetch(API_URLS.getContratos)` (`sava-novos-negocios.html:4912`, `sava-novos-negocios.html:4915`).
- Quando a resposta tem `data.success`, os contratos retornados são salvos em `allContratos` (`sava-novos-negocios.html:4918`, `sava-novos-negocios.html:4919`).
- No primeiro carregamento, se o filtro de mês estiver vazio, o código seleciona automaticamente o mês atual (`sava-novos-negocios.html:4925`, `sava-novos-negocios.html:4928`) e depois chama `filtrarContratosPorMes()` (`sava-novos-negocios.html:4932`).

### Filtro Mensal e Renderização

- Sem filtro de mês, `filtrarContratosPorMes()` renderiza `allContratos` diretamente (`sava-novos-negocios.html:4949`, `sava-novos-negocios.html:4950`).
- Com mês selecionado, a função cria `filtered` a partir de `allContratos.filter(...)` (`sava-novos-negocios.html:4956`).
- Em seguida, a tela é renderizada com `renderContratos(filtered)` (`sava-novos-negocios.html:4966`).
- Dentro de `renderContratos(contratos)`, o índice usado nos cards vem do array recebido pela função, por meio de `contratos.forEach(function (c, idx) { ... })` (`sava-novos-negocios.html:4983`, `sava-novos-negocios.html:5000`).
- Esse índice é guardado em `grouped[s].push({ contrato: c, index: idx })` (`sava-novos-negocios.html:5003`) e depois usado como `idx` nos botões (`sava-novos-negocios.html:5019`).

### Botão "Ver Detalhes"

- Para contratos que não estão em status aprovável, o botão é montado como `onclick="abrirModalContrato(' + idx + ', false)"` (`sava-novos-negocios.html:5049`).
- Para contratos aguardando aprovação ou revisão, os botões "Conferir e Aprovar", "Aprovar Revisão" e "Solicitar Revisão" usam a mesma passagem de `idx` (`sava-novos-negocios.html:5041`, `sava-novos-negocios.html:5044`, `sava-novos-negocios.html:5046`).
- Portanto, o mesmo caminho de índice afeta tanto "Ver Detalhes" quanto ações de aprovação/revisão.

### Modal de Contrato

- O markup do modal de contrato está em `contratoModal` (`sava-novos-negocios.html:2557`).
- Os campos visíveis do popup são preenchidos por IDs como `modalContratoCliente`, `modalContratoArea`, `modalContratoTipo`, `modalContratoData` e `modalContratoAdvogado` (`sava-novos-negocios.html:2589`, `sava-novos-negocios.html:2593`, `sava-novos-negocios.html:2599`, `sava-novos-negocios.html:2603`, `sava-novos-negocios.html:2608`).
- `abrirModalContrato(index, abrirRevisao)` grava o índice em `currentContratoIndex` (`sava-novos-negocios.html:5079`, `sava-novos-negocios.html:5080`).
- Em seguida, a função busca o contrato com `var c = allContratos[index]` (`sava-novos-negocios.html:5082`).
- O modal preenche os dados a partir desse `c`, incluindo nome do cliente, área, tipo, data, advogado e link do Drive (`sava-novos-negocios.html:5084`, `sava-novos-negocios.html:5092`).
- O histórico também é renderizado a partir de `c.historico` (`sava-novos-negocios.html:5099`, `sava-novos-negocios.html:5103`).

### Ações Depois do Modal

- A aprovação usa `allContratos[currentContratoIndex]` para montar o payload enviado a `aprovarContrato` (`sava-novos-negocios.html:5171`, `sava-novos-negocios.html:5173`, `sava-novos-negocios.html:5187`).
- O payload de aprovação inclui `contrato_id`, `cliente_nome`, `cliente_email`, `link_drive` e status do contrato obtido pelo índice atual (`sava-novos-negocios.html:5191`, `sava-novos-negocios.html:5195`).
- A solicitação de revisão também usa `allContratos[currentContratoIndex]` e envia `contrato_id`, `cliente_nome`, `advogado_nome` e observação (`sava-novos-negocios.html:5223`, `sava-novos-negocios.html:5225`, `sava-novos-negocios.html:5243`, `sava-novos-negocios.html:5247`).

## Code References

- `sava-novos-negocios.html:3781` - Objeto `API_URLS` onde ficam as rotas externas.
- `sava-novos-negocios.html:3790` - Rota `get-contratos` usada para carregar a lista de contratos.
- `sava-novos-negocios.html:3902` - Função `navigateTo()`.
- `sava-novos-negocios.html:3912` - Navegação para a tela de contratos dispara `carregarContratos()`.
- `sava-novos-negocios.html:4915` - Fetch de contratos.
- `sava-novos-negocios.html:4919` - Resposta de contratos é armazenada em `allContratos`.
- `sava-novos-negocios.html:4925` - Primeiro carregamento seleciona automaticamente o mês atual.
- `sava-novos-negocios.html:4956` - Filtro mensal cria um novo array `filtered`.
- `sava-novos-negocios.html:4966` - Array filtrado é enviado para `renderContratos(filtered)`.
- `sava-novos-negocios.html:5000` - Índice `idx` é calculado sobre o array recebido em `renderContratos`.
- `sava-novos-negocios.html:5049` - Botão "Ver Detalhes" passa esse `idx` para `abrirModalContrato`.
- `sava-novos-negocios.html:5082` - Modal usa o índice recebido para acessar `allContratos[index]`.
- `sava-novos-negocios.html:5173` - Aprovação também lê `allContratos[currentContratoIndex]`.
- `sava-novos-negocios.html:5225` - Revisão também lê `allContratos[currentContratoIndex]`.

## Architecture Documentation

O arquivo é uma aplicação HTML única com HTML, CSS e JavaScript inline. A seção de contratos usa estado global no browser:

- `allContratos`: array completo retornado pela rota `get-contratos`.
- `currentContratoIndex`: índice usado pelo modal e pelas ações posteriores.
- `renderContratos(contratos)`: renderiza o kanban a partir do array recebido, que pode ser o completo ou um array filtrado.
- `abrirModalContrato(index, abrirRevisao)`: sempre interpreta `index` como posição dentro de `allContratos`.

Fluxo observado:

`navigateTo('screenContratos')` -> `carregarContratos()` -> `fetch(getContratos)` -> `allContratos = data.contratos` -> `filtrarContratosPorMes()` -> `renderContratos(filtered ou allContratos)` -> botão chama `abrirModalContrato(idx)` -> modal lê `allContratos[idx]`.

Quando `renderContratos()` recebe `allContratos`, o índice do card e o índice usado pelo modal apontam para o mesmo array. Quando recebe `filtered`, o índice do card aponta para o array filtrado, mas o modal lê o array completo.

## Open Questions

- O formato e a ordenação exata retornados pelo webhook `get-contratos` não foram verificados nesta pesquisa.
- O backend/workflow do n8n que cria e lista contratos não foi inspecionado.
- Não foi executado teste em navegador com dados reais de Carmem/Tadeu; a conclusão acima vem da leitura estática do fluxo no arquivo HTML.
