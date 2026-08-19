---
title: Novidades de agosto
date: 2026-08-18
summary: Cadastro guiado em etapas, filtros na lista de contratos, progresso no portal por tipo de serviço, ciclo de vida dos dados após a baixa e convites por e-mail com link seguro.
tags:
  - contratos
  - portal
  - privacidade
---

Agosto concentrou melhorias na experiência do operador e das partes envolvidas no contrato — do cadastro à entrega, passando pelo acompanhamento no portal e pelo tratamento dos dados após a baixa.

## Cadastro de contratos em etapas

Abrir ou editar um contrato na área interna agora segue um assistente claro, passo a passo.

### O problema antigo

O pedido reunia muitos campos de uma vez — partes, tipo de serviço, descrição, anexos e honorários — sem uma ordem evidente. Operadores novos tinham dúvida sobre o que preencher primeiro; erros de validação (documento inválido, beneficiário incompleto) só apareciam no fim.

### A solução

A janela de cadastro virou um assistente em três passos: **identificação das partes**, **tipo do serviço** e **descrição do pedido**. Cada etapa valida o essencial antes de avançar. O contratante informa documento (CPF ou CNPJ) e e-mail; o beneficiário continua opcional no início.

### O que muda

- Fluxo guiado com botões **Avançar** e **Voltar** entre os passos
- Validação de CPF/CNPJ e e-mail do contratante no primeiro passo
- Beneficiário pode ser indicado depois — o cadastro inicial admite só o contratante
- Honorários calculados automaticamente no rodapé, visíveis em todo o fluxo

### Saiba mais

- [Pedido e valores](/contratos/pedido)
- [Como abrir um contrato](/aprender/abrir-contrato)

## Lista de contratos com filtros

Encontrar um contrato específico na área interna deixou de depender de rolar a tabela inteira.

### O problema antigo

Com o volume de contratos crescendo, a lista mostrava tudo de uma vez. Para achar um pedido pelo número do serviço, pelo nome do cliente ou pela data prevista, o operador precisava vasculhar manualmente — lento e propenso a erro em dias de pico.

### A solução

A lista de contratos agora aceita filtros combinados. Você restringe por número do serviço, cliente, status e data prevista; a tabela atualiza com o que bate com os critérios.

### O que muda

- Filtros na própria tela de contratos — sem exportar planilha
- Combinação de critérios (ex.: status + data prevista)
- Busca no servidor: resultados consistentes mesmo com muitos registros
- Mensagem **Nenhum contrato encontrado** quando os filtros não retornam linhas

### Saiba mais

- [Lista de contratos](/telas/contratos/lista)
- [Como abrir um contrato](/aprender/abrir-contrato)

## Portal com progresso por tipo de serviço

Depois da ativação, contratante e beneficiário acompanham etapas que fazem sentido para aquele serviço — trânsito ou outro.

### O problema antigo

O andamento do serviço não tinha representação clara no portal. Sem saber em que fase estava o caso, o beneficiário recorria a mensagens ou ligações para perguntar se a defesa já tinha sido anexada ou se o documento estava pronto.

### A solução

O stepper do portal passou a refletir as **etapas do tipo de serviço** contratado. Trânsito mostra marcos como Conteúdo analisado, Defesa gerada e Aguardando julgamento; Outro segue Pedido recebido, Documento elaborado e Concluído. O badge na lista interna usa o mesmo rótulo da etapa atual.

### O que muda

- Stepper visível no portal para contratos ativos
- Etapas diferentes para trânsito e para outros serviços documentais
- Operador atualiza o andamento na área interna; o beneficiário vê a mudança no portal
- Download de documentos do dossiê disponível conforme as regras de cada fase

### Saiba mais

- [Portal](/telas/portal/)
- [Progresso e notificações](/contratos/progresso)
- [Como acompanhar etapas](/aprender/acompanhar-etapas)

## Privacidade após a baixa

Quando o serviço é encerrado, a plataforma cuida da entrega de documentos e do ciclo de vida dos dados pessoais.

### O problema antigo

Após a baixa, o operador precisava montar manualmente o pacote de documentos e o relatório de tratamento para o titular. Não havia fluxo automático de entrega nem prazo definido para anonimização dos dados do caso.

### A solução

Ao dar baixa no contrato, a Anexus gera o **relatório de tratamento** (PDF com a linha do tempo do caso), monta o **pacote ZIP** com os documentos do dossiê e agenda a **anonimização** após o prazo de retenção. Titular e controlador recebem por e-mail quando o envio está configurado.

### O que muda

- Relatório de tratamento gerado automaticamente na baixa
- ZIP com dossiê e relatório enviado ao titular e ao controlador
- Anonimização agendada — dados deixam de identificar a pessoa após o prazo
- Cartão de ciclo de vida visível na área interna para contratos baixados

### Saiba mais

- [Ciclo de vida dos dados](/privacidade/ciclo-de-vida-dos-dados)
- [Como ver o dossiê](/aprender/ver-dossie)

## Convites por e-mail com link seguro

O beneficiário recebe um convite para acessar o portal — sem PDF oficial anexado no e-mail.

### O problema antigo

Enviar o contrato em PDF por e-mail expunha o documento a cópias fora da plataforma e dificultava saber se a pessoa certa tinha acessado. Antes da baixa, o PDF oficial ainda não existe — o convite precisava levar ao lugar certo sem confundir com documento final.

### A solução

Após a ativação do contrato, a plataforma envia e-mail ao beneficiário com o **link temporário** do portal (`/portal/c/{token}`). A pessoa acompanha etapas e dossiê sem login. O documento oficial só fica disponível depois da baixa.

### O que muda

- Convite por e-mail com link direto ao portal — não exige conta
- PDF oficial **não** vai anexado no convite de aceite
- Operador pode reenviar o link pela área interna quando houver e-mail cadastrado
- Sem e-mail do beneficiário, não há portal — o operador gerencia internamente

### Saiba mais

- [Portal](/telas/portal/)
- [Como enviar o portal ao beneficiário](/aprender/enviar-convite)
- [Documentos e acesso](/telas/portal/documentos)

## Em breve

Itens já visíveis na plataforma ou descritos no Guia, com implementação ainda em andamento.

### O problema antigo

Visitantes e operadores não tinham um lugar único para saber o que já funciona hoje e o que ainda está chegando — dúvidas sobre Locação, FAQ pública e assinatura com certificado digital.

### A solução

Estes itens aparecem no cadastro ou na documentação como **previstos**. A opção Locação já está no assistente de cadastro, mas o fluxo completo ainda não está disponível.

### O que muda

- **Locação** como tipo de serviço — opção visível no cadastro; pipeline e honorários em progresso
- Página pública de **perguntas frequentes** — rascunho no Guia; rota no app em breve
- **Assinatura com certificado ICP-Brasil** — aceite eletrônico interno já funciona; ICP em progresso

### Saiba mais

- [Status de implementação](/referencia/status-implementacao)
- [Tipos de serviço](/tipos-de-servico/)
