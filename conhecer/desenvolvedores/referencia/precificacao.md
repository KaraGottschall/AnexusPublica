---
title: Referência — Precificação
description: Infrações RENAINF, cotação de honorários e tipos de serviço
---

# Referência — Precificação

Endpoints de apoio ao cadastro e precificação. Teoria: [Precificação](/precificacao/), [Parâmetros trânsito](/referencia/parametros-precificacao-transito).

Auth **entregue:** JWT + `screens.contracts`. Auth **alvo:** JWT ou chave com `pricing:read` / `domains:read`.

## Tipos de serviço

```http
GET /api/domains/service-types
```

Lista serviços disponíveis para `serviceType` no cadastro (`Traffic`, `Other`, …).

| Item | Valor |
|------|-------|
| Escopo alvo | `domains:read` |
| Cobrança | — |
| Status | **entregue** |

## Infrações de trânsito (RENAINF)

```http
QUERY /api/domains/traffic/infractions
```

Corpo:

```json
{ "search": "502" }
```

Resposta: array com `codigo`, `desdobramento`, `label`, `gravidade`, `valorMultaEfetiva`.

Uso típico: autocomplete no ERP antes de criar contrato.

| Item | Valor |
|------|-------|
| Escopo alvo | `pricing:read` |
| Status | **entregue** |

## Cotação de honorários

```http
QUERY /api/pricing/traffic/quote
```

Corpo:

```json
{
  "codigo": "502-0",
  "desdobramento": 0,
  "instance": "DefesaPrevia"
}
```

Resposta:

| Campo | Descrição |
|-------|-----------|
| `fees` | Honorário calculado |
| `valorBaseGravidade` | Base CTB art. 258 |
| `ready` | `false` se infração sem valor base |

Fórmula comercial: [Precificação trânsito](/precificacao/transito). Parâmetros internos: [Referência — parâmetros](/referencia/parametros-precificacao-transito).

| Item | Valor |
|------|-------|
| Escopo alvo | `pricing:read` |
| Cobrança | — (não duplica honorário do contrato) |
| Status | **entregue** |

## Instâncias (`instance`)

Valores enum string, ex.: `DefesaPrevia`, `Jari`, `Cetran`, `IndicacaoRealCondutor` — multiplicadores conforme tabela comercial.

## Próximo

- [Referência — Contratos](/desenvolvedores/referencia/contratos)
- [Primeiros passos](/desenvolvedores/primeiros-passos)
- [Preços e limites](/desenvolvedores/precos-e-limites)

[← Referência da API](/desenvolvedores/referencia/)
