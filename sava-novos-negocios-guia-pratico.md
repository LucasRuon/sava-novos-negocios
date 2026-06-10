# Guia Pratico - Sistema SAVA Novos Negocios

Este guia foi feito para consulta dos usuarios do sistema. Ele explica como usar cada area e o que acontece automaticamente durante o fluxo, sempre do ponto de vista operacional.

## 1. Para que serve o sistema

O sistema organiza o fluxo de novos negocios da SAVA, desde a captacao de um lead ate o cadastro do negocio, acompanhamento no CRM, geracao/conferencia de contratos e envio para assinatura.

Ele possui tres areas principais:

1. **Formularios**: cadastro de novos negocios e captacao de leads.
2. **CRM Leads**: acompanhamento dos leads e oportunidades.
3. **Contratos**: conferencia, aprovacao, revisao e acompanhamento dos contratos.

## 2. Acesso ao sistema

### Criar conta

1. Abra o sistema.
2. Clique em **Cadastre-se**.
3. Preencha:
   - Nome completo
   - E-mail corporativo `@sava.adv.br`
   - Cargo
4. Clique em **Criar Conta**.
5. Depois da conta criada, volte para a tela de login.

Importante: a criacao de conta so e permitida com e-mail corporativo `@sava.adv.br`. E-mails de outros dominios nao conseguem criar conta nem acessar o sistema.

### Entrar

1. Na tela inicial, informe seu e-mail.
2. Clique em **Entrar**.
3. O sistema abre a area de **Formularios**.

Depois do login, o sistema identifica seu nome e cargo nas telas internas.

## 3. Area Formularios

Na area **Formularios**, escolha qual fluxo deseja iniciar:

- **Negocio Avulso**
- **Negocio de Partido**
- **Captacao de Leads**

Use os botoes no topo do formulario para alternar entre esses tipos.

## 4. Cadastro de Negocio Avulso

Use **Negocio Avulso** quando se tratar de uma contratacao pontual, sem caracteristica recorrente/de partido.

### Passo a passo

1. Clique em **Negocio Avulso**.
2. Em **Dados do Negocio**, informe:
   - natureza do negocio;
   - organizacao interna;
   - tipo de pessoa;
   - area de atuacao;
   - numero do processo, se houver;
   - parte adversa, se houver;
   - escopo de atuacao;
   - resumo da negociacao.
3. Em **Honorarios e Valores**, escolha o tipo de honorarios:
   - Pro Labore;
   - Ad Exitum;
   - Pro Labore + Ad Exitum.
4. Preencha os valores e condicoes de pagamento que aparecerem na tela.
5. Revise a **Clausula de Honorarios para o Contrato**.
6. Em **Dados de Quem Negociou**, informe:
   - tipo de indicacao;
   - responsavel pela indicacao;
   - se havera participacao financeira de quem indicou;
   - responsavel interno pela negociacao;
   - parceiro externo, se houver;
   - se havera participacao financeira do parceiro.
7. Em **Dados do Cliente**, preencha:
   - nome;
   - CPF ou CNPJ;
   - telefone;
   - e-mail;
   - endereco completo.
8. Em **Abertura de Pasta (ADVWin)**, preencha:
   - advogado responsavel;
   - coordenador;
   - socio responsavel;
   - se existem documentos pendentes;
   - se e processo estrategico;
   - data de entrada;
   - objeto da acao;
   - tipo de prazo.
9. Informe se o contrato ja foi assinado fisicamente:
   - **Nao, seguir com assinatura digital**;
   - **Sim, ja assinou**.
10. Clique em **Enviar Cadastro**.

### O que o sistema faz automaticamente

Depois do envio, o sistema registra o novo negocio nos controles internos e encaminha as informacoes para organizacao do caso.

Quando o contrato **ainda nao foi assinado fisicamente**, o sistema pode:

- registrar o negocio na base geral;
- registrar a movimentacao nos controles de contratos avulsos;
- gerar um contrato a partir de modelo, quando a area permitir geracao automatica;
- preencher o contrato com os dados do cliente, do negocio e dos honorarios;
- deixar o contrato disponivel para conferencia;
- criar uma pasta no Drive com o nome do cliente;
- salvar uma copia do contrato na pasta criada;
- enviar e-mail interno comunicando nova abertura de pasta;
- enviar e-mail para documentos pendentes, quando essa opcao for marcada;
- avisar o financeiro quando houver Pro Labore ou Pro Labore + Ad Exitum.

Quando o contrato **ja foi assinado fisicamente**, o sistema segue um caminho mais simples:

- registra o negocio;
- registra o contrato como ja assinado;
- cria uma pasta no Drive para organizacao do caso;
- solicita ao financeiro a geracao de cobranca;
- nao envia o contrato para assinatura digital.

Observacao: para areas como Criminal e Tributario, o fluxo identificado registra o negocio, mas nao segue a mesma geracao automatica de contrato usada nos demais casos.

## 5. Cadastro de Negocio de Partido

Use **Negocio de Partido** quando se tratar de uma contratacao recorrente ou com acompanhamento continuado.

### Passo a passo

1. Clique em **Negocio de Partido**.
2. Preencha os dados principais do negocio.
3. Informe os honorarios e condicoes comerciais.
4. Preencha os dados de quem negociou.
5. Preencha os dados do cliente.
6. Informe os dados para abertura de pasta.
7. Preencha os campos especificos de partido, quando aparecerem:
   - robo de monitoramento;
   - criterio de reajuste;
   - periodo de vigencia;
   - responsaveis por setor, quando for pessoa juridica.
8. Informe se o contrato ja foi assinado fisicamente.
9. Clique em **Enviar Cadastro**.

### O que o sistema faz automaticamente

Depois do envio, o sistema:

- registra o negocio na base geral;
- registra a movimentacao nos controles de contratos de partido;
- encaminha as informacoes para abertura e organizacao da pasta;
- envia comunicacao interna sobre a nova abertura;
- solicita documentos pendentes ao cliente, se essa opcao foi marcada;
- solicita ao financeiro a cobranca, conforme as condicoes preenchidas;
- quando aplicavel, encaminha o contrato para conferencia e posterior assinatura.

## 6. Captacao de Leads

Use **Captacao de Leads** quando ainda nao existe negocio fechado, mas ha um possivel cliente a acompanhar.

### Passo a passo

1. Clique em **Captacao de Leads**.
2. Preencha:
   - nome completo;
   - telefone;
   - e-mail;
   - area de interesse;
   - data sugerida para reuniao;
   - horario preferido;
   - observacoes ou resumo do caso;
   - providencias para a secretaria;
   - origem do lead.
3. Clique em **Cadastrar Lead**.

### O que o sistema faz automaticamente

Depois do cadastro:

- o lead entra no CRM como **Novo Lead**;
- a pendencia financeira inicia como **Nao**;
- as informacoes de contato, origem, area, agendamento e observacoes ficam registradas;
- a secretaria recebe um e-mail avisando sobre o novo lead;
- quem cadastrou o lead tambem recebe copia da comunicacao.

## 7. CRM Leads

A area **CRM Leads** serve para acompanhar oportunidades comerciais.

### Como consultar leads

1. Clique em **CRM Leads**.
2. Aguarde o carregamento dos cards.
3. Use a busca para procurar um lead por nome ou e-mail.
4. Clique em **Atualizar** para recarregar a lista.

### Etapas do funil

Os leads aparecem em colunas:

- Novo Lead
- Contato Realizado
- Reuniao Agendada
- Proposta Enviada
- Negocio Fechado
- Perdido

Para mudar um lead de etapa, arraste o card para a coluna desejada.

### Ver e editar detalhes do lead

1. Clique em **Detalhes** no card do lead.
2. Revise os dados principais.
3. Atualize, se necessario:
   - area de interesse;
   - status;
   - valor da proposta;
   - pendencia financeira;
   - notas do CRM.
4. Clique em **Salvar Alteracoes**.

### Marcar pendencia financeira

Ao abrir os detalhes do lead, marque **Pendencia Financeira** quando existir algum ponto financeiro que precise de atencao. Leads com pendencia aparecem destacados no CRM.

### Converter lead em negocio

1. No card ou nos detalhes do lead, clique em **+ Negocio** ou **Converter em Negocio**.
2. O sistema abre o formulario de **Negocio Avulso**.
3. Nome, telefone, e-mail e area do lead sao preenchidos automaticamente.
4. Complete os campos obrigatorios restantes.
5. Clique em **Enviar Cadastro**.

Importante: a conversao apenas preenche o formulario. O negocio so e registrado depois do envio do cadastro.

### Relatorios do CRM

Na opcao **Relatorios**, o sistema mostra:

- quantidade de leads por etapa;
- comparativo entre leads e negocios fechados;
- origem dos leads;
- areas de interesse.

Na parte superior do CRM, tambem aparecem indicadores de total de leads, negocios fechados, taxa de conversao e pendencias financeiras.

## 8. Contratos

A area **Contratos** e usada para acompanhar contratos gerados, conferir conteudo, solicitar revisao ou aprovar envio para assinatura.

### Como consultar contratos

1. Clique em **Contratos**.
2. Aguarde o carregamento dos contratos.
3. Use o filtro de mes para consultar contratos de um periodo especifico.
4. Clique em **Atualizar** para recarregar.

### Status dos contratos

Os contratos ficam organizados nas colunas:

- Aguardando Aprovacao
- Revisao Solicitada
- Em Assinatura
- Assinados

Cada card mostra informacoes como cliente, area, tipo, advogado responsavel e data de geracao.

### Conferir contrato

1. Clique em **Copiar Link** ou abra os detalhes do contrato.
2. O sistema copia o link do contrato.
3. Cole o link no navegador para abrir o documento.
4. Confira o conteudo antes de aprovar.

### Aprovar contrato e enviar para assinatura

1. Abra o contrato que esta aguardando aprovacao.
2. Confira os dados do contrato.
3. Selecione o **Responsavel pela Assinatura (Sava)**.
4. Clique em **Aprovar e Enviar**.

Depois da aprovacao, o sistema:

- atualiza o contrato para **Em Assinatura**;
- gera uma versao em PDF do contrato;
- envia o documento para assinatura digital;
- inclui o cliente como signatario;
- inclui o responsavel SAVA selecionado como signatario;
- envia os avisos de assinatura automaticamente;
- guarda o link de assinatura para acompanhamento.

### Solicitar revisao do contrato

1. Abra o contrato.
2. Clique em **Solicitar Revisao**.
3. Selecione o **Responsavel pela Assinatura (Sava)**.
4. Escreva uma observacao clara sobre o que precisa ser ajustado.
5. Clique em **Confirmar Revisao**.

Depois da solicitacao, o sistema:

- muda o contrato para **Revisao Solicitada**;
- registra a observacao da revisao;
- envia e-mail ao responsavel pela assinatura selecionado;
- inclui no e-mail o cliente, quem solicitou, a observacao e o link do contrato;
- pode enviar aviso por WhatsApp quando esse canal estiver ativo.

### Quando o contrato e assinado

Depois que todos os signatarios concluem a assinatura digital:

- o contrato passa para **Assinado**;
- a equipe recebe aviso de contrato assinado;
- o aviso informa o nome do contrato;
- o documento assinado pode ser considerado valido e arquivado conforme o procedimento interno.

Se apenas uma parte assinou e ainda faltam outros signatarios, o sistema aguarda as assinaturas restantes antes de marcar como **Assinado**.

### Historico do contrato

Dentro dos detalhes do contrato, consulte o **Historico do Contrato** para verificar interacoes anteriores, aprovacoes, revisoes e observacoes registradas.

## 9. Listas e nomes novos

Alguns campos usam listas internas, como:

- advogado responsavel;
- coordenador;
- socio responsavel;
- responsavel pela indicacao;
- responsavel interno pela negociacao;
- parceiro externo.

Quando a opcao **Outros** aparecer:

1. Selecione **Outros**.
2. Digite o nome no campo exibido.
3. Clique em **Adicionar**.
4. O sistema inclui o nome na lista e ja deixa a opcao selecionada.

## 10. Comunicacoes automaticas

### Novo lead

Quando um lead e cadastrado, a secretaria e o usuario que cadastrou recebem e-mail com as principais informacoes do lead:

- quem cadastrou;
- nome;
- telefone;
- e-mail;
- area de interesse;
- agendamento, se houver;
- observacoes;
- origem;
- providencias para a secretaria.

### Nova abertura de pasta

Quando um novo negocio e enviado, a equipe interna recebe e-mail avisando sobre a nova abertura de pasta. A comunicacao inclui informacoes gerais, dados do cliente, dados do negocio e dados para organizacao interna.

### Documentos pendentes

Quando o usuario marca **Documentos Pendentes? Sim** e descreve os documentos faltantes, o sistema envia uma solicitacao ao cliente com a lista dos documentos necessarios. A equipe interna e o usuario que cadastrou tambem podem receber copia.

### Financeiro

Quando ha necessidade de cobranca, o financeiro recebe uma solicitacao com dados do cliente e da pasta para gerar boleto, Pix ou outro meio de pagamento aplicavel.

Essa solicitacao aparece especialmente quando:

- o negocio possui Pro Labore ou Pro Labore + Ad Exitum;
- o contrato ja foi assinado fisicamente e precisa seguir para cobranca.

### Contrato para aprovacao

Quando o sistema gera contrato automaticamente, a equipe responsavel recebe aviso de que existe um novo contrato para conferencia e aprovacao.

### Revisao de contrato

Quando uma revisao e solicitada, o responsavel selecionado recebe e-mail com a observacao de ajuste e o link do contrato.

### Contrato assinado

Quando a assinatura digital e concluida por todos os signatarios, a equipe recebe e-mail informando que o contrato foi assinado.

## 11. Organizacao automatica de documentos

Conforme o tipo de cadastro e a situacao do contrato, o sistema pode:

- criar pasta no Drive com o nome do cliente;
- gerar contrato a partir de modelo;
- preencher o contrato com dados do formulario;
- liberar o contrato para edicao/conferencia;
- exportar o contrato em PDF;
- salvar o arquivo na pasta criada;
- registrar o contrato para acompanhamento na area **Contratos**.

Quando o contrato ja foi assinado fisicamente, o sistema registra essa condicao e nao conduz o documento pelo fluxo normal de assinatura digital.

## 12. Regras praticas importantes

- **Criminal e Tributario**: esses casos podem nao gerar contrato automaticamente como os demais. O cadastro fica registrado, mas a preparacao contratual pode exigir tratativa manual.
- **Previdenciario PF**: segue modelo especifico de contrato.
- **Demais avulsos PF/PJ**: seguem modelo geral de contrato avulso.
- **Contrato ja assinado**: pula assinatura digital e entra como assinado no acompanhamento.
- **Contrato nao assinado**: segue para geracao, conferencia, aprovacao e assinatura digital.
- **Documentos pendentes**: so geram solicitacao ao cliente quando o campo e marcado como **Sim** e os documentos sao descritos.
- **Pro Labore**: aciona comunicacao ao financeiro para cobranca.

## 13. Fluxo completo fora do sistema

Esta parte mostra o que acontece depois que o usuario clica nos botoes do sistema. Ela mistura etapas automaticas e tarefas manuais da equipe.

### Quando um lead e cadastrado

1. O usuario cadastra o lead na area **Captacao de Leads**.
2. O lead aparece no CRM como **Novo Lead**.
3. A secretaria recebe e-mail avisando que existe um novo lead.
4. O usuario que cadastrou tambem recebe copia do e-mail.
5. A secretaria ou o responsavel comercial consulta os dados do lead.
6. A equipe entra em contato com o possivel cliente pelo canal adequado.
7. Se houver data e horario sugeridos, a equipe usa essas informacoes para organizar a reuniao.
8. Depois do contato, o responsavel atualiza o status do lead no CRM.
9. Se o lead virar oportunidade real, o usuario clica em **Converter em Negocio**.
10. O sistema preenche os dados basicos no formulario de negocio.
11. O usuario completa o restante do cadastro e envia o novo negocio.

### Quando um novo negocio e enviado sem contrato assinado

1. O usuario preenche o formulario e marca **Nao, seguir com assinatura digital**.
2. Ao clicar em **Enviar Cadastro**, o sistema registra o novo negocio.
3. A equipe interna recebe e-mail informando a nova abertura de pasta.
4. O sistema cria uma pasta no Drive para organizar os arquivos do cliente.
5. O sistema gera o contrato, quando a area permite contrato automatico.
6. O contrato fica disponivel para conferencia.
7. O responsavel acessa o link do contrato pelo e-mail recebido ou pela area **Contratos**.
8. O responsavel confere todos os dados do contrato.
9. Se precisar ajustar texto, dados ou clausulas, o responsavel pode editar o contrato diretamente no documento antes da aprovacao.
10. Depois de conferir ou editar, o responsavel volta para a area **Contratos**.
11. Se o contrato estiver correto, clica em **Aprovar e Enviar**.
12. Se o contrato ainda precisar de ajuste, clica em **Solicitar Revisao** e descreve claramente o que deve ser corrigido.

### Quando existem documentos pendentes

1. No formulario, o usuario marca **Documentos Pendentes? Sim**.
2. O usuario descreve exatamente quais documentos faltam.
3. Depois do envio do cadastro, o cliente recebe e-mail solicitando os documentos.
4. A equipe interna tambem recebe copia da solicitacao.
5. O cliente deve responder ao e-mail encaminhando os documentos solicitados.
6. Ao receber os documentos, a secretaria ou o responsavel pelo caso deve salvar os arquivos na pasta do cliente no Drive.
7. O responsavel deve conferir se os documentos recebidos correspondem ao que foi solicitado.
8. Se ainda faltar algo, a equipe deve cobrar o cliente novamente pelo canal adequado.
9. Quando estiver tudo completo, os documentos devem ficar organizados na pasta do caso para continuidade da abertura e acompanhamento.

### Quando o financeiro e acionado

1. Se o negocio envolve Pro Labore, Pro Labore + Ad Exitum ou contrato ja assinado, o financeiro recebe e-mail solicitando a geracao de cobranca.
2. O e-mail informa os dados do cliente e da pasta.
3. O financeiro confere os dados recebidos.
4. O financeiro gera o boleto, Pix ou outra forma de pagamento aplicavel.
5. O financeiro encaminha a cobranca ao cliente.
6. O financeiro acompanha o pagamento conforme o procedimento interno.
7. Se houver inadimplencia, o financeiro trata a pendencia pelo fluxo financeiro da SAVA.

### Quando o contrato e aprovado para assinatura

1. O responsavel aprova o contrato no sistema.
2. O contrato passa para **Em Assinatura**.
3. O cliente recebe e-mail com o link para assinar o contrato.
4. O responsavel SAVA escolhido tambem recebe e-mail para assinatura.
5. O cliente acessa o link recebido.
6. O cliente assina o contrato digitalmente.
7. O responsavel SAVA acessa o link recebido.
8. O responsavel SAVA tambem assina o contrato.
9. Enquanto faltar alguma assinatura, o contrato continua aguardando conclusao.
10. Quando todos assinam, o contrato passa para **Assinado**.
11. A equipe recebe e-mail informando que o contrato foi assinado.
12. A equipe deve salvar ou conferir o documento assinado na pasta do cliente, conforme o procedimento interno.

### Quando uma revisao de contrato e solicitada

1. O usuario abre o contrato na area **Contratos**.
2. Clica em **Solicitar Revisao**.
3. Seleciona o responsavel pela assinatura SAVA.
4. Escreve uma observacao objetiva sobre o que precisa mudar.
5. O contrato passa para **Revisao Solicitada**.
6. O responsavel selecionado recebe e-mail com a solicitacao de revisao.
7. O e-mail inclui o nome do cliente, quem solicitou, a observacao e o link do contrato.
8. O responsavel acessa o contrato pelo link.
9. O responsavel faz os ajustes necessarios no documento.
10. Depois do ajuste, o contrato deve ser conferido novamente.
11. Quando estiver correto, o responsavel retorna ao sistema e aprova a revisao para seguir com a assinatura.

### Quando o contrato ja foi assinado fisicamente

1. No cadastro do negocio, o usuario marca **Sim, ja assinou**.
2. O sistema registra o negocio como contrato ja assinado.
3. O contrato nao segue para assinatura digital.
4. O sistema cria ou prepara a organizacao da pasta do cliente.
5. O financeiro recebe solicitacao de cobranca, quando aplicavel.
6. A equipe deve inserir na pasta do cliente a copia do contrato fisico assinado.
7. A equipe tambem deve inserir os demais documentos recebidos do cliente.
8. A abertura e organizacao da pasta seguem conforme o procedimento interno da SAVA.

### Abertura e organizacao da pasta

1. O sistema envia a comunicacao de nova abertura de pasta para a equipe interna.
2. A pasta do cliente e criada no Drive quando o fluxo aplicavel executa essa etapa.
3. O advogado, secretaria ou responsavel pelo caso deve acessar a pasta.
4. O responsavel deve salvar na pasta:
   - documentos enviados pelo cliente;
   - contrato gerado;
   - contrato assinado, quando houver;
   - comprovantes ou arquivos relevantes ao caso.
5. Quando a abertura depender de ADVWin ou outro controle interno, a equipe deve usar os dados do formulario para concluir o cadastro no respectivo sistema.
6. A pasta deve permanecer organizada para que qualquer pessoa da equipe consiga consultar o caso depois.

## 14. Links uteis

Use estes links apenas quando fizerem parte da sua rotina ou quando a gestao orientar o acesso.

- Pasta geral de novos negocios no Drive: https://drive.google.com/drive/folders/10gGDxH_byq37gV5_rB29YG_p3QNN973q
- Controle geral de novos negocios: https://docs.google.com/spreadsheets/d/1tN3kXkDPEToNy63V4yD3CrpdJf7JU0vgEQz5Q88qLmE/edit
- Controle operacional de leads e contratos: https://docs.google.com/spreadsheets/d/1Nd-hQTINwripUiM6zKLB9xgZ24Pu21PIX5LKb-z9SSo/edit
- Controle de contratos avulsos e de partido: https://docs.google.com/spreadsheets/d/11s_kwnicjG-2C7hH4yj81sipnF-4U9fXQiMqBeWJiBI/edit

Observacao: o link individual de cada contrato aparece no e-mail recebido e tambem no card do contrato dentro da area **Contratos**.

## 15. Checklist antes de enviar um negocio

- O tipo correto foi selecionado: Avulso ou Partido.
- A natureza do negocio foi marcada.
- A area de atuacao esta correta.
- CPF/CNPJ foi preenchido corretamente.
- Escopo e resumo da negociacao estao claros.
- Honorarios e valores foram revisados.
- Clausula de honorarios foi conferida.
- Dados de indicacao e negociacao foram preenchidos.
- Dados do cliente estao completos.
- Advogado, coordenador e socio responsavel foram definidos.
- Documentos pendentes foram descritos, se houver.
- Prazo foi informado corretamente.
- Foi marcado se o contrato ja foi assinado fisicamente.

## 16. Checklist antes de aprovar um contrato

- O contrato foi aberto e conferido.
- Cliente, area, tipo e advogado estao corretos.
- O conteudo do contrato esta adequado.
- Historico de revisoes foi consultado.
- Responsavel pela assinatura SAVA foi selecionado.
- Se houver erro, foi solicitada revisao com observacao objetiva.
- Se estiver correto, foi clicado em **Aprovar e Enviar**.

## 17. Boas praticas de uso

- Preencha os campos com o maximo de clareza possivel.
- Use o campo de observacoes para registrar contexto que ajude quem dara continuidade.
- Em documentos pendentes, detalhe exatamente o que falta.
- Antes de aprovar contrato, sempre confira o documento.
- Ao solicitar revisao, escreva uma orientacao objetiva e acionavel.
- Mantenha o CRM atualizado para que os indicadores reflitam a situacao real.
