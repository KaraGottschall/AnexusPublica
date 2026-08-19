---
title: Portal
description: Área pública sem login para o beneficiário acompanhar etapas e dossiê
---

# Portal

O **Portal** é a área pública da Anexus exclusiva do [Beneficiário](/atores/beneficiario): acompanhar **etapas** e baixar o **dossiê**. Não exige conta nem login. O acesso é pelo **link temporário** enviado por e-mail após a ativação do contrato.

O [Contratante](/atores/contratante) **não** usa o portal. Pedido, conferência dos termos, pagamento e gestão ficam na [área interna](/telas/contratos/). A [Anexus](/atores/anexus) é a plataforma; o operador autenticado age ali.

## Endereços

| Caminho | Uso | Documentação |
|---------|-----|--------------|
| `/portal` | Página inicial (colar link ou token) | [Início](/telas/portal/inicio) |
| `/portal/c/{link}` | Contrato ativo: stepper e dossiê | [Dossiê](/telas/portal/dossie), [Token inválido](/telas/portal/token-invalido) |
| `/portal/lgpd` | Formulário público de privacidade (LGPD) | [Privacidade (LGPD)](/telas/portal/lgpd) |

## Do pedido ao dossiê

O operador cria o contrato, confere as informações e **confirma e paga** na área interna. O pagamento ativa e lacra o contrato. Se houver e-mail do beneficiário, a plataforma envia o link do portal. Fluxo: [Documentos e acesso](/telas/portal/documentos) e [Assinatura e integridade](/contratos/assinatura).

Contrato **sem beneficiário** (ou sem e-mail): não há portal. O operador gerencia tudo internamente.

## Como cada parte chega

<PortalAccessFlow />

| Ator | O que é específico |
|------|-------------------|
| **Operador** | Área interna: cadastro, conferência, pagamento, anexos e compartilhamento do link. |
| **Beneficiário (com e-mail)** | Recebe o link após a ativação; vê etapas e dossiê, **sem** assinar nem pagar. |
| **Beneficiário (sem e-mail)** | Sem portal; o operador acompanha o caso na área interna. |
| **Contratante** | Visível só na área interna; não acessa o portal. |

## Etapas na tela

O portal só abre para contrato **ativo**. O stepper mostra as etapas **daquele tipo de serviço**, a partir de **Trabalho iniciado**. Sequência completa: [Progresso e notificações](/contratos/progresso).

## Tokens e links seguros

- Cada token é pessoal e tem validade limitada.
- Reenviar o acesso ao beneficiário **invalida** o token anterior e emite um novo.
- Token inválido, expirado ou de contrato que não está ativo não revela o motivo — a tela trata como não encontrado. Detalhes: [Token inválido](/telas/portal/token-invalido).

## Privacidade (LGPD)

Em todas as telas do portal há acesso a **Privacidade e LGPD** (`/portal/lgpd`), para solicitações de acesso, correção ou exclusão de dados. Ver [Privacidade (LGPD)](/telas/portal/lgpd) e, para o contexto legal e canais, [Como solicitar](/privacidade/solicitacoes).

## Próximo

- [Início](/telas/portal/inicio) — colar link ou token
- [Assinatura e integridade](/contratos/assinatura) — conferência interna, pagamento e lacre
- [Dossiê](/telas/portal/dossie) — documentos do contrato ativo
- [Token inválido](/telas/portal/token-invalido)
- [Privacidade (LGPD)](/telas/portal/lgpd)
- [Documentos e acesso](/telas/portal/documentos)
- [Telas](/telas/) — visão geral das telas documentadas
