# SAVA Novos Negocios

Aplicacao web estatica para operar o fluxo de novos negocios da SAVA. O arquivo principal, `sava-novos-negocios.html`, concentra login, cadastro de negocios, captacao de leads, CRM comercial e acompanhamento de contratos.

## Visao geral

O sistema cobre o fluxo operacional desde a entrada de um lead ate o cadastro do negocio, organizacao documental, conferencia de contrato e envio para assinatura digital.

Areas principais:

- **Formularios**: cadastro de negocio avulso, negocio avulso sem contrato, negocio de partido e captacao de leads.
- **CRM Leads**: funil em Kanban, busca, indicadores, relatorios e conversao de lead em negocio.
- **Contratos**: consulta, filtro por mes, conferencia, aprovacao, solicitacao de revisao e acompanhamento de assinatura.

## Como usar

Abra `sava-novos-negocios.html` em um navegador moderno ou sirva o diretorio como site estatico:

```bash
python3 -m http.server 8080
```

Depois acesse:

```text
http://localhost:8080/sava-novos-negocios.html
```

O app depende dos webhooks externos configurados no proprio HTML. Para uso real, o navegador precisa conseguir acessar os endpoints n8n, Google Drive/Sheets e ZapSign usados pelas automacoes.

## Fluxos do sistema

### Acesso

- Registro de usuarios com nome, e-mail corporativo `@sava.adv.br` e cargo.
- Login por e-mail.
- Persistencia de sessao no navegador.
- Barra interna com nome, cargo e navegacao entre Formularios, CRM Leads e Contratos.

### Formularios

O usuario pode alternar entre quatro tipos de formulario:

- **Negocio Avulso**: cadastro completo para negocio pontual com fluxo de contrato.
- **Negocio Avulso (sem contratos)**: cadastro de negocio sem geracao/fluxo contratual automatico.
- **Negocio de Partido**: cadastro de contratacao recorrente, com campos especificos de vigencia, reajuste, monitoramento e responsaveis.
- **Captacao de Leads**: registro de possivel cliente para acompanhamento comercial.

O formulario de negocio coleta dados de area, natureza, cliente, honorarios, indicacao, negociacao, abertura de pasta, responsaveis internos, documentos pendentes e situacao do contrato. Tambem inclui validacao/formatacao de CPF, CNPJ, telefone e numero de processo.

### Honorarios e contrato

O app trata combinacoes de honorarios como:

- Pro Labore.
- Ad Exitum.
- Pro Labore + Ad Exitum.
- Manutencao anual.
- Valor fixo de exito.

Conforme area, tipo de pessoa, tipo de negocio e honorarios selecionados, o HTML atualiza uma previa da clausula de honorarios do contrato.

Quando o contrato ja foi assinado fisicamente, o usuario pode marcar essa condicao para pular o fluxo de assinatura digital.

### CRM Leads

O CRM exibe leads em colunas de funil:

- Novo Lead.
- Contato Realizado.
- Reuniao Agendada.
- Proposta Enviada.
- Negocio Fechado.
- Perdido.

Recursos disponiveis:

- busca por nome ou e-mail;
- drag and drop para atualizar status;
- indicadores de total de leads, negocios fechados, taxa de conversao e pendencias financeiras;
- modal de detalhes para editar status, area, valor da proposta, pendencia financeira e notas;
- conversao de lead em negocio, preenchendo automaticamente dados basicos do cliente no formulario;
- relatorios por etapa, origem e area de interesse.

### Contratos

A area de contratos lista documentos por status:

- Aguardando Aprovacao.
- Revisao Solicitada.
- Em Assinatura.
- Assinados.

Recursos disponiveis:

- filtro por mes;
- indicadores por status;
- copia de link do contrato no Drive;
- modal de detalhes com cliente, area, tipo, data, responsavel e historico;
- selecao do responsavel SAVA pela assinatura;
- aprovacao e envio para assinatura via ZapSign;
- solicitacao de revisao com observacao obrigatoria.

## Integracoes

O HTML usa webhooks n8n definidos no objeto `API_URLS`:

- `registro`
- `login`
- `novosNegocios`
- `leads`
- `getListas`
- `addNome`
- `getLeads`
- `updateLead`
- `getContratos`
- `aprovarContrato`
- `solicitarRevisao`

As automacoes conectadas a esses webhooks coordenam registros em planilhas, organizacao no Google Drive, comunicacoes internas, geracao/conferencia de contratos e envio para assinatura via ZapSign.

## Arquivos do repositorio

- `sava-novos-negocios.html`: aplicacao principal.
- `sava-novos-negocios-guia-pratico.md`: guia operacional para usuarios.
- `sava-treinamento.html`: material/tela de treinamento relacionado.
- `docs/Contrato Modelo SAVA.docx`: modelo de contrato usado no fluxo documental.
- `SAVA _ Novos Negócios.json`: workflow principal de novos negocios.
- `SAVA - Captação de Leads.json`: workflow de captacao de leads.
- `SAVA - APROVAR Contrato → ZapSign.json`: workflow de aprovacao e envio para assinatura.
- `SAVA - SOLICITAR Revisão de Contrato.json`: workflow de solicitacao de revisao.
- `SAVA - ZapSign Webhook → Contrato Assinado.json`: workflow de retorno de assinatura concluida.

## Manutencao

Ao alterar o sistema, confira estes pontos:

- atualizar o objeto `API_URLS` se algum webhook mudar;
- manter os nomes e formatos de campos alinhados com os workflows n8n;
- revisar a previa da clausula de honorarios quando regras comerciais mudarem;
- manter `sava-novos-negocios-guia-pratico.md` sincronizado com mudancas de interface;
- testar cadastro, CRM e contratos depois de qualquer mudanca em formulario ou payload.
