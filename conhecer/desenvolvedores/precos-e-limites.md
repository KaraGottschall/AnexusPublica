---
title: Preços e limites
description: Honorário por contrato vs acesso à API — o que é cobrado, rate limits e planos de integração
---

# Preços e limites

A API é um **canal de acesso** à mesma plataforma da área interna. A cobrança principal continua sendo o **honorário documental por contrato**, não o fato de usar HTTP em vez da interface.

::: info Status
Rate limit por chave de API é **previsto**. Hoje existem rate limits em validação documental, doc-review e recuperação de senha.
:::

## Princípio: canal não muda honorário

> Abrir contrato, anexar documentos, compartilhar o portal e pagar honorários seguem as mesmas regras de [Precificação](/precificacao/) e [Pedido e valores](/dominios/contratos-pedido). **Não há taxa adicional por usar a API em vez da interface** para operações já cobertas pelo honorário do contrato.

Como diz a documentação de produto: *não importa se o pedido entrou pelo sistema, WhatsApp ou outro canal — o preço não muda depois de definido*. A API entra nessa mesma regra.

## Duas camadas de preço

```
┌─────────────────────────────────────────────────────────┐
│  Plataforma / API (acesso, volume, SLA)                 │  ← opcional; política comercial
├─────────────────────────────────────────────────────────┤
│  Serviço documental (honorário por contrato)            │  ← já existe; igual UI ou API
└─────────────────────────────────────────────────────────┘
```

### Honorário documental (já cobrado hoje)

| Evento | Cobrança |
|--------|----------|
| Cadastrar contrato (preço em aberto) | Ainda não |
| Fechar honorário + pagar (`POST .../pay` → Stripe) | **Honorário do contrato** |
| Ativar contrato após pagamento | Mesmo pagamento — não é taxa separada |
| Nova instância / novo pedido (ex.: recurso JARI) | **Novo honorário** — [Escopo](/precificacao/escopo) |

O que o honorário cobre: [O que o honorário cobre](/precificacao/escopo).

### Acesso à API (política comercial)

Na v1 documentada:

- **Incluído** para quem já opera contratos na plataforma — sem tarifa por chamada para operações de contrato
- **Planos de integração** (futuro, se oferecidos): referem-se a volume, SLA ou recursos premium — **não** duplicam o honorário

## O que não gera cobrança extra via API

| Operação | Cobrança adicional? |
|----------|---------------------|
| `QUERY /api/contracts` (listar) | Não |
| `GET /api/contracts/{id}` | Não |
| `POST /api/contracts` | Não — honorário entra no contrato |
| Anexos, share-portal, cancel, close | Não |
| `QUERY .../quote` (cotação trânsito) | Não — apoio ao pedido, como no formulário |
| `QUERY .../infractions`, `GET .../service-types` | Não |

## Pagamento via API

`POST /api/contracts/{id}/pay` retorna credenciais Stripe (`clientSecret`, `publishableKey`) para o **mesmo valor** `Fees` do contrato. A confirmação ocorre via webhook Stripe — mesmo fluxo da UI.

- **Sandbox:** cartões de teste Stripe
- **Produção:** cobrança real ao titular/contratante

Escopo sensível: `contracts:pay` — conceder só a integrações que realmente iniciam checkout.

## Validador público

`POST /api/validar` é **gratuito** hoje, com rate limit por IP.

Uso em **alta escala** (validação em massa por parceiros) pode virar produto comercial separado — distinto do honorário de contrato. Até lá, tratar como utilitário público.

## Rate limits

Limites protegem estabilidade; não substituem precificação de honorário.

| Superfície | Limite (referência) | Status |
|------------|---------------------|--------|
| Validação documental | Por IP, janela fixa | **Entregue** |
| Doc-review (UI) | Por IP + usuário | **Entregue** |
| Recuperação de senha | Por IP | **Entregue** |
| API key (integração) | Por chave + tenant | **Previsto** |

Resposta `429 Too Many Requests` inclui `Retry-After` quando aplicável.

## O que evitar (política)

- Cobrar por `POST /contracts` **e** honorário no contrato
- Cobrar consulta de status que a UI mostra sem taxa
- Sandbox pago antes de existir valor real de homologação

## Próximo

- [Ambientes](/desenvolvedores/ambientes) — Stripe test vs live
- [Escopos](/desenvolvedores/escopos) — incluindo `contracts:pay`
- [Primeiros passos](/desenvolvedores/primeiros-passos)

[← Voltar a Desenvolvedores](/desenvolvedores/)
