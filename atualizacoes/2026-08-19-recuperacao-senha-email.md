---
title: Recuperação de senha por e-mail
date: 2026-08-19
summary: Quem esqueceu a senha consegue recuperar o acesso sem depender do suporte.
tags:
  - segurança
---
### O problema antigo

Sem fluxo de redefinição, o operador bloqueado precisava pedir ajuda para recuperar a conta — atraso operacional e dependência de terceiros para algo que deveria ser self-service.

### A solução

A tela **Esqueci minha senha** guia em três passos: informar o e-mail cadastrado, confirmar o código recebido por e-mail (OTP) e definir a nova senha. O fluxo respeita limites de tentativas para proteger contra abuso.

### O que muda

- Link **Esqueci minha senha** na tela de login
- Código de verificação enviado ao e-mail da conta
- Nova senha definida na própria plataforma, sem ticket de suporte
- Rate limiting: tentativas excessivas são bloqueadas temporariamente

### Saiba mais

- [Como fazer login](/aprender/fazer-login)
- [Plataforma](/plataforma)
