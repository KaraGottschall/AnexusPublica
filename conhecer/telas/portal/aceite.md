---
title: Conferência e pagamento
description: O operador confirma os termos e paga na área interna
---

# Conferência e pagamento

O aceite dos termos **não** acontece no portal. O operador, na área interna, confere o pedido no **quarto passo** do cadastro (ou na página do contrato) e marca que aceita os termos **em nome do contratante**. Em seguida, **confirma e paga**.

O pagamento dos honorários (Stripe Checkout) também é interno. O retorno fica em `/app/contratos/{id}`. Após a confirmação, o contrato fica **ativo** e lacrado. Se houver e-mail do [beneficiário](/atores/beneficiario), a plataforma envia o link do portal.

Detalhes: [Assinatura e integridade](/contratos/assinatura) e [Lista e operações](/telas/contratos/lista).

## Próximo

- [Dossiê](/telas/portal/dossie) — o que o beneficiário vê depois da ativação
- [Pedido e valores](/contratos/pedido) — o que entra no cadastro

[← Voltar ao Portal](/telas/portal/)
