---
title: Segurança, validação e pagamentos
date: 2026-08-19
summary: Recuperação de senha por e-mail, validador público de integridade documental, pagamento com Stripe e compartilhamento do portal ao beneficiário.
tags:
  - segurança
  - validação
  - pagamentos
  - portal
---

Novas ferramentas reforçam a confiança na plataforma: recuperar acesso à conta, conferir se um PDF ainda é íntegro, pagar honorários com cartão e enviar o portal ao beneficiário com um clique.

## Recuperação de senha por e-mail

Quem esqueceu a senha consegue recuperar o acesso sem depender do suporte.

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

## Validador público de integridade documental

Qualquer pessoa pode conferir se um PDF emitido pela Anexus ainda é íntegro — sem login.

### O problema antigo

Depois que um contrato ou relatório saía da plataforma, não havia forma pública de verificar se o arquivo foi alterado, reimpresso ou adulterado. A confiança dependia só do visual ou de contato com o escritório.

### A solução

A página **Integridade documental** (`/validar`) recebe o PDF e analisa lacres, hashes por seção e rastreabilidade forense. O resultado mostra se o documento é íntegro, adulterado ou não reconhecido como emitido pela Anexus.

### O que muda

- Validação disponível para visitantes — não exige conta
- Três desfechos claros: íntegro, adulterado, não reconhecido
- Detalhes de proveniência quando o documento é vinculado a um contrato
- Mensagem específica quando o PDF não corresponde a nenhum documento da plataforma

### Saiba mais

- [Validação forense](/referencia/engenharia/validacao-forense)
- [Assinatura e integridade](/contratos/assinatura)

## Pagamento de honorários com Stripe

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

## Compartilhamento do portal ao beneficiário

O operador envia o link do portal ao beneficiário direto da área interna, após a ativação.

### O problema antigo

Depois de pagar e ativar, o operador não tinha um atalho claro para compartilhar o acesso com o beneficiário. Copiar tokens manualmente ou depender de fluxos antigos gerava atrito e atraso na comunicação com o titular.

### A solução

Na página do contrato, o operador usa **Compartilhar portal** para reenviar o link por e-mail ao beneficiário cadastrado. O sistema registra quando o acesso foi compartilhado e mantém o token válido para o acompanhamento das etapas.

### O que muda

- Ação **Compartilhar portal** na área interna, após contrato ativo
- Reenvio por e-mail quando há endereço do beneficiário
- Registro de compartilhamento para auditoria interna
- Anexos do contrato disponíveis para download na área interna

### Saiba mais

- [Como enviar o portal ao beneficiário](/aprender/enviar-convite)
- [Portal](/telas/portal/)
- [Documentos e acesso](/telas/portal/documentos)
