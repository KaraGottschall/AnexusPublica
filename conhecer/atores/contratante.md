---
title: Contratante
description: Quem contrata; o operador confirma os termos e paga na área interna
---

# Contratante

O **Contratante** é quem firma o contrato e a quem se prestam os serviços no acordo — o cliente do fluxo contratual. **Não** acessa o [Portal](/telas/portal/).

Pode ser o próprio usuário autenticado ou o cliente dele. Em qualquer caso, o operador confirma os termos **em nome do contratante** e paga os honorários na área interna.

## O que faz

- Fornece informações necessárias ao serviço contratado.
- É a parte em cujo nome o operador aceita os termos e paga os honorários.
- Não acompanha o andamento no portal — a gestão fica com o operador.

### Com beneficiário

Quando há [Beneficiário](/atores/beneficiario) no serviço:

- O operador declara, na conferência, ter autorização e consentimento (LGPD) do beneficiário em nome do contratante.
- O contratante continua obrigado a repassar cópia do contrato ao beneficiário, quando a relação assim exigir.

### Sem beneficiário

A declaração de privacidade cobre apenas os dados do próprio contratante. Sem e-mail de terceiro, **não há portal**.

## Papel na LGPD

O contratante é a **parte contratual**. Papéis no tratamento: [Papéis no tratamento](/privacidade/papeis).

## Na área interna

- O operador cadastra nome, documento e e-mail do contratante no pedido.
- A conferência dos termos e o pagamento acontecem em `/app/contratos` — ver [Lista e operações](/telas/contratos/lista) e [Assinatura e integridade](/contratos/assinatura).
- O **documento oficial** para download e envio só fica disponível após a baixa.

## Ciclo no sistema

| Momento | O que acontece |
|---------|----------------|
| Cadastro | O operador cadastra o contratante (cliente) pela área interna |
| Contrato | O contratante é informado ao criar o contrato |
| Conferência | O operador aceita os termos em nome do contratante |
| Pagamento | Honorários na área interna; o contrato passa a ativo e o PDF é lacrado ([assinatura e integridade](/contratos/assinatura)) |
| Após ativação | Se houver beneficiário com e-mail, o portal é compartilhado com ele |
| Documento oficial | A **baixa** (operada pelo usuário autenticado) **libera** o PDF oficial |

## Relação com os outros atores

- Com a **Anexus**: relação contratual — prestação do serviço pela plataforma e cobrança de honorários.
- Com o **Beneficiário**: o contratante viabiliza o serviço em favor do beneficiário.

[← Voltar aos Atores](/atores/)
