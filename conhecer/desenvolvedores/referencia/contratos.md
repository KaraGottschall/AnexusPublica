---
title: Referência — Contratos
description: Endpoints de contratos — listagem, CRUD, anexos, pagamento e portal
---

# Referência — Contratos

Base: `/api/contracts`. Domínio de produto: [Contratos](/dominios/contratos), [Pedido e valores](/dominios/contratos-pedido).

Auth **entregue:** JWT + policy `screens.contracts`. Auth **alvo:** JWT ou chave com escopos `contracts:*`.

## Listagem

```http
QUERY /api/contracts
```

Corpo opcional (filtros):

```json
{
  "serviceNumber": "2026-001",
  "clientName": "Silva",
  "lifecycle": "Active",
  "expectedDate": "2026-09-30"
}
```

| Item | Valor |
|------|-------|
| Escopo alvo | `contracts:read` |
| Status | **entregue** |

## Detalhe

```http
GET /api/contracts/{id}
```

Retorna `ContractDto` com partes, serviço, honorários, anexos, lifecycle, token de portal quando existir.

## Criar

```http
POST /api/contracts
```

Corpo: `CreateContractCommand` — `clientName`, `clientDocument`, `clientEmail`, `expectedDate`, `serviceType`, `beneficiary*`, `traffic` ou `other`, `attachments` opcional.

| Campo | Notas |
|-------|-------|
| `serviceType` | `Traffic`, `Other` (`Rental` ainda indisponível) |
| `traffic` | Obrigatório se trânsito — código infração, instância, órgão |
| Honorário | Calculado no servidor conforme [Precificação](/precificacao/) |

| Item | Valor |
|------|-------|
| Escopo alvo | `contracts:write` |
| Cobrança | Honorário registrado no contrato (cobrado em `/pay`) |
| Status | **entregue** |

## Atualizar

```http
PUT /api/contracts/{id}
PATCH /api/contracts/{id}/beneficiario
```

| Item | Valor |
|------|-------|
| Escopo alvo | `contracts:write` |
| Status | **entregue** |

## Anexos

```http
POST /api/contracts/{id}/attachments     (multipart: type, file)
GET  /api/contracts/{id}/attachments/{attachmentId}
DELETE /api/contracts/{id}/attachments/{attachmentId}
```

| Item | Valor |
|------|-------|
| Campo `type` | Restrito por `serviceType` |
| Limite | Tamanho máximo por regra de domínio |
| Escopo alvo | `contracts:attachments` |
| Status | **entregue** |

## Pagamento

```http
POST /api/contracts/{id}/pay
```

Corpo opcional:

```json
{
  "deviceLocation": {
    "status": "granted",
    "latitude": -23.55,
    "longitude": -46.63,
    "accuracyMeters": 10
  }
}
```

Resposta: `clientSecret`, `publishableKey` (Stripe). Honorário zero pode ativar sem checkout.

| Item | Valor |
|------|-------|
| Escopo alvo | `contracts:pay` |
| Cobrança | Honorário do contrato via Stripe |
| Status | **entregue** |

Confirmação: webhook `POST /api/stripe/webhook`.

## Portal

```http
POST /api/contracts/{id}/share-portal
```

Gera ou expõe `portalToken` para link `/portal/c/{token}`.

| Item | Valor |
|------|-------|
| Escopo alvo | `contracts:portal` |
| Status | **entregue** |

## Encerrar e cancelar

```http
POST /api/contracts/{id}/close
POST /api/contracts/{id}/cancel
```

| Item | Valor |
|------|-------|
| Escopo alvo | `contracts:write` |
| Status | **entregue** |

## LGPD pós-baixa

```http
GET /api/contracts/{id}/treatment-report
GET /api/contracts/{id}/data-package
```

Download PDF/ZIP após baixa do serviço.

| Item | Valor |
|------|-------|
| Escopo alvo | `contracts:read` |
| Status | **entregue** (geração LaTeX em Development pode exigir TeX Live) |

## Endpoints de desenvolvimento

Disponíveis apenas em `Development` / `Testing`:

- `POST /api/contracts/demo/lgpd-reset`
- `POST /api/contracts/{id}/data-lifecycle/force-anonymize`
- `POST /api/contracts/{id}/data-lifecycle/advance`
- `POST /api/contracts/{id}/data-lifecycle/run`

**Não** fazem parte da API pública v1.

## Próximo

- [Referência — Precificação](/desenvolvedores/referencia/precificacao)
- [Primeiros passos](/desenvolvedores/primeiros-passos)
- [Escopos](/desenvolvedores/escopos)

[← Referência da API](/desenvolvedores/referencia/)
