---
title: Pagamento de honorários com Stripe
date: 2026-08-19
summary: A confirmação e o pagamento do contrato na área interna passam a usar cartão via Stripe.
tags:
  - pagamentos
  - contratos
---

A confirmação e o pagamento do contrato na área interna passam a usar cartão via Stripe.

### O problema antigo

O fluxo de pagamento ainda não estava integrado de forma confiável à ativação do contrato. Referências a métodos antigos (como PIX) confundiam o operador sobre como concluir o pedido e liberar o portal.

### A solução

Após conferir as informações no assistente de cadastro, o operador paga os honorários com **cartão** (Stripe). O webhook confirma o pagamento e **ativa** o contrato automaticamente — lacrando o PDF e liberando o envio do portal ao beneficiário.

### O que muda

- Pagamento único na área interna, após o passo **Conferir informações**
- Cartão de crédito ou débito via Stripe — sem PIX na plataforma
- Ativação automática do contrato após confirmação do pagamento
- Status de pagamento visível na página do contrato

### Saiba mais

- [Como pagar honorários](/aprender/pagar-honorarios)
- [Pedido e valores](/contratos/pedido)
- [Assinatura e integridade](/contratos/assinatura)
