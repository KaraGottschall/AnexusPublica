---
title: Lista e operações
description: KPIs, tabela com accordions e ações sobre contratos na área interna da Anexus
---

# Lista e operações

Na **lista de contratos** da [área interna](/atores/anexus), o operador consulta indicadores, a tabela operacional e as ações de cada serviço.

O título da tela é **Contratos**, com o subtítulo *Indicadores, lista operacional e ações da área interna.* Após cada operação, uma faixa de confirmação aparece no topo por alguns segundos — por exemplo, *Contrato cadastrado.* ou *Contrato atualizado.* Cada linha tem o atalho **Abrir contrato**, que leva à página `/app/contratos/{id}`.

## Onde acessar

A tela fica no menu lateral da **área interna**, após o login do operador Anexus.

## Indicadores no topo

Quatro KPIs resumem a carteira de contratos:

| Indicador | O que mostra |
|-----------|--------------|
| **Contratos totais** | Quantidade de contratos registrados no sistema |
| **Contratos ativos** | Contratos assinados e em operação (serviço não baixado nem cancelado) |
| **Faturamento total** | Soma dos honorários de contratos assinados |
| **Faturamento do mês** | Honorários de contratos **assinados no mês calendário atual** |

Os valores de faturamento referem-se apenas a contratos **ativos** (pagos) — rascunhos não entram nesses totais.

### O que a pessoa vê

<ContractsKpiDemo />

## Contratos em andamento

Abaixo dos KPIs, a seção **Contratos em andamento** lista os serviços, com o subtítulo *Lista operacional com detalhes e ações por linha.* Os contratos aparecem ordenados pelo **Nº do serviço**, do mais recente para o mais antigo. Se ainda não houver nenhum, a tabela mostra **Nenhum contrato cadastrado.** Com filtros ativos e nenhum resultado, a mensagem passa a **Nenhum contrato encontrado.**

O botão **Cadastrar novo contrato** abre a janela de [pedido e valores](/contratos/pedido), agora com quatro passos (o último é **Conferir informações**). Cada linha é um **accordion**: o resumo fica visível na linha; ao expandir, o operador vê o detalhe do pedido e o [Beneficiário](/atores/beneficiario) quando já informado. **Abrir contrato** leva à página de detalhe.

## Filtros

Acima da tabela, quatro campos filtram a lista:

| Filtro | O que busca |
|--------|-------------|
| **Nº do serviço** | Identificador interno (por exemplo, o número do contrato) |
| **Cliente** | Nome ou razão social do contratante |
| **Status** | Fase do ciclo de vida (Rascunho, Documento gerado, Pendente, Assinado / Ativo, Baixado, Cancelado) — ou **Todos** |
| **Data prevista** | Prazo acordado para protocolo ou entrega |

Os filtros combinam: o operador vê só os contratos que atendem a todos os critérios preenchidos.

## Cadastro e edição

**Cadastrar novo contrato** e **Editar** abrem uma **janela** com assistente em três passos. O título é **Cadastrar novo contrato** ou **Editar contrato**, com a descrição *Identifique as partes, escolha o serviço e descreva o pedido.*

O rodapé da janela mostra os honorários (somente leitura) e os botões **Cancelar** e **Avançar**. No último passo, **Avançar** vira **Criar contrato** (cadastro) ou **Salvar alterações** (edição).

### Passo 1 — Identificação das partes

| Campo | Observação |
|-------|------------|
| **Nome ou razão social (contratante)** | Sempre |
| **Documento (CPF ou CNPJ)** | Sempre — validado conforme o tipo de documento |
| **E-mail do contratante** | Sempre — canal do convite de aceite |
| **Desejo indicar um beneficiário** | Interruptor; desligado por padrão |

Com o interruptor ligado, aparecem **Beneficiário** (nome), **CPF do beneficiário** e **E-mail do beneficiário**. Um ícone de ajuda explica que o beneficiário é o titular dos dados e do serviço. Sem identificação completa do beneficiário, o contrato não segue.

O beneficiário também pode ficar para depois: o cadastro inicial admite só o contratante.

### Passo 2 — Tipo do serviço

O campo **Tipo de serviço** oferece **Trânsito**, **Outro** e **Locação**. Catálogo: [Tipos de serviço](/tipos-de-servico/).

**Locação** está em progresso para implementação. Se o operador escolher essa opção, o passo seguinte informa que a funcionalidade ainda não está disponível — não é possível criar o contrato nessa modalidade.

### Passo 3 — Descrição do serviço

Os campos mudam conforme o tipo escolhido. Regras de negócio do pedido — AIT no fechamento, cadastro parcial, formação do preço — estão em [Pedido e valores](/contratos/pedido).

| Campo | Quando aparece |
|-------|----------------|
| **Instância** | Trânsito (Defesa prévia, Indicação de real condutor, JARI, CETRAN) |
| **Órgão autuador** | Trânsito (DETRAN, PRF, Prefeitura) |
| **Código da infração** | Trânsito |
| **Pacote comercial** | Outro |
| **Descrição do serviço** | Outro (opcional) |
| **Data máxima de entrega** | Trânsito e Outro |
| **Anexos** | Trânsito e Outro — tipos disponíveis mudam com o tipo de serviço |
| **Honorários** | Sempre no rodapé, calculados automaticamente (somente leitura) |

### Anexos na janela

No campo **Anexos**, o operador escolhe o **tipo do documento** e clica em **Adicionar** para selecionar o arquivo. Cada item aparece como *tipo — nome do arquivo*, com botão para excluir.

Formatos aceitos: PDF, PNG, JPEG ou WebP, com no máximo 10 MB. Os tipos disponíveis dependem do tipo de serviço escolhido:

| Tipo de serviço | Tipos de anexo |
|-----------------|----------------|
| **Trânsito** | AIT (auto de infração), CNH do condutor, CNH do real condutor, RENAVAM, Comprovante |
| **Outro** | Documento do caso, Comprovante, Outro |

Se o operador mudar o tipo de serviço, anexos incompatíveis saem da lista.

Os anexos ficam **somente nesta janela** — a linha expandida da tabela não lista os arquivos. O [dossiê do serviço](/contratos/#dossie-do-servico) é o lugar em que as partes consultam os documentos depois.

### Quando a edição não está disponível

Não é possível editar o pedido depois que o contrato está **lacrado** (aceite concluído) nem quando está **baixado** ou **cancelado**. Enquanto o aceite ainda está pendente, o pedido pode ser alterado.

Clique em **Cadastrar novo contrato** no preview abaixo para abrir a janela, como na tela real.

### O que a pessoa vê — cadastro

<ContractsListCadastroDemo />

## Accordion da linha

Ao expandir uma linha, o operador vê um resumo do pedido:

- Nº do serviço
- Tipo de serviço e instância (trânsito) ou pacote comercial (outro)
- Órgão autuador e código da infração — só em trânsito
- Descrição — só em outro, quando preenchida
- Honorários
- Pré-assinatura Anexus, quando o operador já conferiu e pagou
- Beneficiário, documento e e-mail — quando já informados
- Em telas estreitas, também a data prevista (coluna oculta da tabela)

O link do portal do beneficiário fica na **página do contrato**, não na lista. Contratos **baixados** exibem também o cartão de ciclo de vida dos dados (relatório e documentos entregues).

### O que a pessoa vê — accordion

<ContractAccordionDemo contract-id="ct-aguardando-1" />

## Cliente e beneficiário na linha

Os nomes de **Cliente** e **Beneficiário** na tabela são clicáveis. Abrem um card com o papel da pessoa e o número do serviço:

| Parte | O que o card mostra |
|-------|---------------------|
| **Cliente** | Contratante do serviço, prazo previsto e mês/ano em que o contrato foi cadastrado |
| **Beneficiário** | Titular, documento e e-mail — ou *Sem documento ou e-mail cadastrados.* |

Em computador com mouse, o card aparece ao passar o ponteiro; em tela de toque, abre ao tocar o nome.

## Colunas da tabela

| Coluna | Conteúdo |
|--------|----------|
| (expansão) | Seta para abrir ou recolher o accordion |
| **Cliente** | [Contratante](/atores/contratante) vinculado ao serviço — nome abre o card |
| **Beneficiário** | Nome do titular, quando já cadastrado; em telas estreitas a coluna some e o dado reaparece no accordion |
| **Data prevista** | Prazo acordado para protocolo ou entrega; em telas estreitas a coluna some e o dado reaparece no accordion |
| **Status** | Badge da fase atual do contrato (ver abaixo) |
| **Ações** | Botões de operação sobre o contrato (ver abaixo) |

O **Nº do serviço** aparece no accordion e no card do cliente ou do beneficiário — não é uma coluna própria.

## Status

A coluna de status exibe um **badge** da fase atual — o mesmo mecanismo de transparência do [stepper](/contratos/progresso), para o operador ver (e as partes acompanharem no portal) em que ponto o serviço está. Em contrato **ativo**, o badge mostra a etapa do **tipo de serviço** daquele contrato (trânsito ou outro).

| Badge | Significado |
|-------|-------------|
| **Rascunho** | Pedido salvo; ainda não pago |
| **Documento gerado** | Contrato montado |
| **Pendente** | Fluxo antigo ainda não migrado — o operador confirma e paga na página do contrato |
| **Assinado / Ativo** | Pagamento concluído; PDF lacrado — quando ainda não há etapa de serviço marcada |
| Etapa do serviço | Só em contrato ativo: o rótulo segue o tipo — trânsito (Conteúdo analisado, Defesa gerada, Anexada no processo, Aguardando julgamento, Julgado) ou outro (Pedido recebido, Documento elaborado, Entregue, Concluído) |
| **Baixado** | Serviço liquidado e entregue pelo operador |
| **Cancelado** | Contrato encerrado sem conclusão do serviço |

Enquanto o contrato está em rascunho, o badge de etapa de serviço **não** aparece — o foco é concluir a conferência e o pagamento.

### O que a pessoa vê — exemplos

Alterne entre **Pendente** e **Ativo com etapa** para ver como os badges mudam na linha da tabela:

<ContractRowStatusDemo />

## Ações

A coluna de ações reúne os botões disponíveis conforme o estado do contrato. Nem todos aparecem ao mesmo tempo. Em telas largas, os botões ficam na própria linha; em telas estreitas, ficam no menu **Ações**. Contratos **baixados** ou **cancelados** não exibem ações.

| Ação | Quando está disponível | O que faz |
|------|------------------------|-----------|
| **Abrir contrato** | Sempre | Vai para `/app/contratos/{id}` — anexos, pagamento, portal e LGPD |
| **Editar** | Contrato ainda não lacrado e não encerrado | Abre a janela e altera o [pedido](/contratos/pedido) — tipo de serviço, prazo, anexos etc. |
| **Dar baixa** | Contrato ativo | Pede confirmação (*Dar baixa no contrato?*), registra a entrega do serviço e **libera o PDF oficial** |
| **Cancelar** | Qualquer estágio, exceto baixado ou cancelado | Pede confirmação (*Cancelar contrato?*) e encerra o contrato sem baixa de serviço |

Na página do contrato, o operador também **paga** rascunhos e **reenvia o portal** ao beneficiário quando há e-mail.

## Assinatura Anexus no PDF

Ao confirmar e pagar, o **operador pré-assina** o PDF; o lacre ocorre na ativação. Formato da linha de assinatura e dados registrados: [Assinatura e integridade](/contratos/assinatura#dados-usados-em-cada-etapa).

## Relação com outras telas

| Tela / fluxo | Conexão |
|--------------|---------|
| [Pedido e valores](/contratos/pedido) | Formulário de cadastro e edição do contrato, incluindo anexos |
| [Assinatura e integridade](/contratos/assinatura) | Pré-assinatura, aceite, lacre, prévia inválida e hash SHA-256 |
| [Progresso e notificações](/contratos/progresso) | Badges de etapa e stepper dentro do detalhe do contrato |
| [Portal](/telas/portal/) | Dossiê do beneficiário após a ativação |
| [Tipos de serviço](/tipos-de-servico/) | Trânsito, outro e locação (em progresso) — campos e etapas |
| [Dossiê](/contratos/#dossie-do-servico) | Upload e consulta de documentos do serviço |

Para demos e URLs locais, veja [Fixtures de contratos](/referencia/fixtures-contratos).

[← Voltar a Contratos](/telas/contratos/)
