---
title: Documentos e acesso
description: Como e quando cada parte acessa o contrato e o dossiê
---

# Documentos e acesso

Esta página explica **o que** cada ator vê e **quando**, no [Portal](/telas/portal/) e na área interna. Complementa a visão dos [Atores](/dominios/atores). O dossiê é a **fonte da verdade** documental do serviço — o que entra e o que sai do caso fica registrado ali.

## Tipos de documento

| Tipo | O que é | Quem produz |
|------|---------|-------------|
| **Contrato (PDF)** | Instrumento do acordo; pré-assinado pelo operador na conferência; lacrado com hash após o pagamento. Download e envio **oficial** só após a baixa — ver [Prévia inválida e documento oficial](/dominios/contratos-assinatura#previa-invalida-e-documento-oficial) | Sistema (a partir dos dados do contrato) |
| **Documentos do dossiê** | Anexos do processo (identidade, autos, peças, comprovantes, etc.) | Operador (upload na área interna) |

## Matriz por parte

| Capacidade / documento | Operador (interno) | Contratante | Beneficiário (portal) |
|------------------------|:---------------:|:-----------:|:---------------------:|
| Ver contrato antes do pagamento | Sim | Não (sem portal) | Não |
| Aceitar os termos | Sim (em nome do contratante) | Não no portal | Não |
| Pagar honorários | Sim | Não no portal | Não |
| Ver contrato após o lacre | Sim | Só na área interna | Sim (se houver e-mail e link) |
| Baixar contrato **antes da baixa** | Instrumento lacrado | — | **Prévia inválida** |
| Baixar contrato **após a baixa** | PDF oficial | — | PDF **oficial** |
| Ver dossiê | Upload e gestão na página do contrato | Não | Após contrato **ativo** |
| Receber e-mail de portal | — | Não | Após a ativação (se houver e-mail) — **link**; **sem** PDF oficial |
| Receber PDF oficial por e-mail | — | Após a **baixa** | Após a **baixa** (se houver e-mail) |

## Por fase do contrato

<ContractPhasesFlow />

### 1. Rascunho

- Só o **operador** age: cria contrato, edita escopo, associa beneficiário (opcional), anexa arquivos.
- Ainda não há link de portal.

### 2. Conferência

- No quarto passo do cadastro, o operador revisa as informações e aceita os termos **em nome do contratante**.
- Pode **salvar rascunho** ou **confirmar e pagar**.

### 3. Pagamento e lacre

- O pagamento ocorre na área interna (Stripe Checkout ou ativação imediata se o honorário for zero).
- Após a confirmação, o sistema lacra o PDF e o contrato fica **ativo**.
- O hash fica registrado na plataforma; o PDF oficial **ainda não** é enviado às partes externas.

### 4. Portal do beneficiário

- Se houver e-mail do beneficiário, a plataforma envia o **link** do portal — **sem** anexo do PDF oficial.
- Sem e-mail, não há portal; o operador continua na área interna.

### 5. Operação e baixa

- O beneficiário vê stepper e dossiê no portal.
- O operador faz upload, baixa, entrega e encerramento na área interna.
- **Após a baixa**: o PDF **oficial** fica disponível no dossiê para download e o envio por e-mail passa a ser permitido.

## Por canal de acesso

| Canal | O que permite | Documentos listados? |
|-------|---------------|:--------------------:|
| Área interna | Cadastro, conferência, pagamento, anexos, baixa | Sim |
| E-mail de portal (beneficiário) | Acompanhar dossiê — **sem** PDF oficial anexo | Sim, contrato ativo (contrato = prévia inválida até a baixa) |
| E-mail após a baixa | Download e envio do **PDF oficial** | Sim — contrato oficial |

Resumo do que o portal “vê”:

| Situação | Documentos | Download do contrato | Pode pagar? |
|----------|:----------:|----------------------|:-----------:|
| Token de contrato que não está ativo | Não (404) | — | Não |
| Beneficiário + ativo, sem baixa | Sim | Prévia inválida | Não |
| Beneficiário + baixado | Mensagem de encerrado ou dossiê conforme a política vigente | **Oficial**, se o dossiê permanecer | Não |
| Operador + qualquer fase | Sim (área interna) | Instrumento lacrado após o pagamento | Sim, enquanto rascunho |

## Casos especiais

| Situação | Comportamento |
|----------|---------------|
| Contrato **sem** beneficiário | Sem e-mail de portal; o operador gerencia tudo internamente |
| Beneficiário **sem** e-mail | Sem portal automático |
| Reenvio do acesso | Links antigos deixam de funcionar; um novo token é emitido |
| Contrato **baixado** | Portal de contrato ativo deixa de abrir; PDF **oficial** na área interna e, quando aplicável, por e-mail |
| Link inválido ou expirado | Tela genérica de não encontrado (sem detalhar o motivo) — ver [Token inválido](/telas/portal/token-invalido) |

[← Voltar ao Portal](/telas/portal/) · [Dossiê](/telas/portal/dossie) · [Token inválido](/telas/portal/token-invalido) · [Atores](/dominios/atores)
