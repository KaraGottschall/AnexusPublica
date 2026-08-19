---
title: Token inválido
description: O que o portal mostra quando o link de acesso não é válido
---

# Token inválido

Quando alguém abre `/portal/c/{token}` e o sistema **não encontra** um link válido, o portal exibe uma tela genérica de “não encontrado”. O motivo real (expirado, revogado, digitado errado ou nunca existiu) **não é revelado**.

## Quando isso acontece

O portal trata o token como inválido quando:

- o token está vazio ou malformado;
- o token não existe nos links ativos;
- o link está marcado como expirado.

Reenvio do aceite ou revogação manual também invalidam tokens anteriores — quem usar o link antigo vê esta mesma tela. Detalhes: [Tokens e links seguros](/telas/portal/#tokens-e-links-seguros) e [Documentos e acesso](/telas/portal/documentos).

## O que a pessoa vê

A mensagem orienta a usar o **link mais recente** do e-mail de convite, sem detalhar o erro:

<PortalNotFoundDemo />

Para demos e URLs locais, veja [Fixtures do portal](/referencia/fixtures-portal).

[← Voltar ao Portal](/telas/portal/) · [Início](/telas/portal/inicio) · [Documentos e acesso](/telas/portal/documentos)
