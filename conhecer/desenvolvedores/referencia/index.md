---
title: Referência da API
description: Índice da referência REST v1 — OpenAPI, versionamento e mapa de recursos
---

# Referência da API

Detalhe por recurso da API Anexus v1. Política geral: [Desenvolvedores](/desenvolvedores/), [Convenções](/desenvolvedores/convencoes), [Superfícies](/desenvolvedores/superficies).

::: info Status
OpenAPI publicada em produção e autenticação por chave são **previstas**. Em Development local: `/openapi/v1.json` e Swagger UI na API.
:::

## OpenAPI

| Ambiente | Especificação |
|----------|---------------|
| Development (local) | <DevApi field="openapi-url" env="local" /> |
| Sandbox | **previsto** — <DevApi field="openapi-url" env="test" /> |
| Produção | **previsto** — <DevApi field="openapi-url" env="live" /> |

Versionamento: prefixo `v1` na URL OpenAPI; paths REST permanecem em `/api/...`. Breaking changes exigem nova versão documentada e período de depreciação.

## Mapa de recursos

| Recurso | Descrição | Auth integração |
|---------|-----------|-----------------|
| [Contratos](/desenvolvedores/referencia/contratos) | Pedidos, anexos, pagamento, portal | JWT / escopos `contracts:*` |
| [Precificação](/desenvolvedores/referencia/precificacao) | Infrações, cotação, tipos de serviço | JWT / `pricing:read`, `domains:read` |
| [Portal](/desenvolvedores/referencia/portal) | Consulta beneficiário por token | Token de link (sem API key) |
| [Validação](/desenvolvedores/referencia/validacao) | Integridade forense de PDF | Anônimo |

## Controllers (backend)

Referência cruzada com `Anexus.Api/Controllers`:

| Controller | Rota base | Doc |
|------------|-----------|-----|
| `ContractsController` | `/api/contracts` | [Contratos](/desenvolvedores/referencia/contratos) |
| `TrafficPricingController` | `/api/pricing/traffic` | [Precificação](/desenvolvedores/referencia/precificacao) |
| `TrafficDomainsController` | `/api/domains/traffic` | [Precificação](/desenvolvedores/referencia/precificacao) |
| `ServiceTypesController` | `/api/domains/service-types` | [Precificação](/desenvolvedores/referencia/precificacao) |
| `PortalController` | `/api/portal` | [Portal](/desenvolvedores/referencia/portal) |
| `DocumentValidationController` | `/api/validar` | [Validação](/desenvolvedores/referencia/validacao) |

## Em breve

- Coleção Postman / Insomnia exportada do OpenAPI
- SDK oficial (não comprometido)
- Webhooks de saída (`contract.activated`, etc.)

## Relacionado

- [Engenharia — Validação forense](/referencia/engenharia/validacao-forense) — algoritmo do validador
- [Status de implementação](/referencia/status-implementacao)

[← Voltar a Desenvolvedores](/desenvolvedores/)
