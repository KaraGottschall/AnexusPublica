---
title: Superfícies
description: Matriz de endpoints — autenticação, escopo, cobrança e status de implementação
---

# Superfícies

Visão consolidada de **todas** as superfícies HTTP da API Anexus: integração M2M, UI, portal, público e webhooks.

Legenda de status:

| Status | Significado |
|--------|-------------|
| **entregue** | Disponível no backend atual |
| **previsto** | Descrito como alvo; ainda não implementado |

## API de integração (JWT hoje → escopos alvo)

Auth **entregue:** JWT + `screens.contracts`. Auth **alvo:** JWT **ou** chave com escopos.

### Contratos — `/api/contracts`

| Método | Path | Escopo alvo | Cobrança | Status |
|--------|------|-------------|----------|--------|
| `QUERY` | `/api/contracts` | `contracts:read` | — | entregue |
| `GET` | `/api/contracts/{id}` | `contracts:read` | — | entregue |
| `POST` | `/api/contracts` | `contracts:write` | honorário no contrato | entregue |
| `PUT` | `/api/contracts/{id}` | `contracts:write` | — | entregue |
| `PATCH` | `/api/contracts/{id}/beneficiario` | `contracts:write` | — | entregue |
| `POST` | `/api/contracts/{id}/attachments` | `contracts:attachments` | — | entregue |
| `GET` | `/api/contracts/{id}/attachments/{attachmentId}` | `contracts:attachments` | — | entregue |
| `DELETE` | `/api/contracts/{id}/attachments/{attachmentId}` | `contracts:attachments` | — | entregue |
| `POST` | `/api/contracts/{id}/pay` | `contracts:pay` | honorário (Stripe) | entregue |
| `POST` | `/api/contracts/{id}/share-portal` | `contracts:portal` | — | entregue |
| `POST` | `/api/contracts/{id}/close` | `contracts:write` | — | entregue |
| `POST` | `/api/contracts/{id}/cancel` | `contracts:write` | — | entregue |
| `GET` | `/api/contracts/{id}/treatment-report` | `contracts:read` | — | entregue |
| `GET` | `/api/contracts/{id}/data-package` | `contracts:read` | — | entregue |
| `POST` | `/api/contracts/demo/lgpd-reset` | — | — | dev only |
| `POST` | `/api/contracts/{id}/data-lifecycle/*` | — | — | dev only |

Detalhe: [Referência — Contratos](/desenvolvedores/referencia/contratos).

### Precificação e domínios

| Método | Path | Escopo alvo | Cobrança | Status |
|--------|------|-------------|----------|--------|
| `QUERY` | `/api/domains/traffic/infractions` | `pricing:read` | — | entregue |
| `QUERY` | `/api/pricing/traffic/quote` | `pricing:read` | — | entregue |
| `GET` | `/api/domains/service-types` | `domains:read` | — | entregue |

Detalhe: [Referência — Precificação](/desenvolvedores/referencia/precificacao).

## Somente área interna (fora da API pública v1)

| Método | Path | Auth hoje | API pública v1 |
|--------|------|-----------|----------------|
| `GET` | `/api/home/summary` | JWT + `screens.home` | não |
| `GET/PATCH` | `/api/settings` | JWT + `screens.settings` | não |
| `GET` | `/api/lgpd/requests` | JWT + `screens.settings` | não |
| `POST` | `/api/doc-review/issues` | JWT | não |

## Auth — `/api/auth`

| Método | Path | Uso | API pública v1 |
|--------|------|-----|----------------|
| `POST` | `/api/auth/login` | UI | anônimo |
| `POST` | `/api/auth/register` | UI | anônimo |
| `POST` | `/api/auth/refresh` | UI | anônimo |
| `POST` | `/api/auth/password-reset/*` | UI | anônimo |
| `GET` | `/api/auth/me` | UI | JWT |
| `GET/DELETE` | `/api/auth/sessions` | UI | JWT |

Não substituído por API key — login humano permanece JWT.

## Portal — `/api/portal` (sem API key)

| Método | Path | Auth | Status |
|--------|------|------|--------|
| `QUERY` | `/api/portal/c/{token}` | token de link | entregue |
| `POST` | `/api/portal/lgpd` | anônimo | entregue |
| `QUERY` | `/api/portal/c/{token}/documents/{documentId}` | token de link | entregue |

Detalhe: [Referência — Portal](/desenvolvedores/referencia/portal).

## Validador — `/api/validar` (sem API key)

| Método | Path | Auth | Status |
|--------|------|------|--------|
| `POST` | `/api/validar` | anônimo + rate limit IP | entregue |

Detalhe: [Referência — Validação](/desenvolvedores/referencia/validacao).

## Webhook Stripe — `/api/stripe/webhook`

| Método | Path | Auth | Status |
|--------|------|------|--------|
| `POST` | `/api/stripe/webhook` | assinatura `Stripe-Signature` | entregue |

Integração máquina-a-máquina com Stripe — não usa JWT nem API key Anexus.

## Gaps doc → código (API pública)

| Item | Status |
|------|--------|
| Entidade e persistência `ApiKey` | previsto |
| Middleware dual auth (JWT + <DevApi field="prefix-family" />) | previsto |
| Policies por escopo | previsto |
| Validação chave ↔ ambiente (test/live) | previsto |
| UI <SettingsPath section="desenvolvedor" item="api-keys" /> | previsto |
| Rate limit por chave | previsto |
| OpenAPI em produção | previsto |
| Aliases GET/POST para endpoints QUERY | previsto |

Lista completa: [Status de implementação — API pública](/referencia/status-implementacao#api-publica).

## Próximo

- [Primeiros passos](/desenvolvedores/primeiros-passos)
- [Referência da API](/desenvolvedores/referencia/)
- [Escopos](/desenvolvedores/escopos)

[← Voltar a Desenvolvedores](/desenvolvedores/)
