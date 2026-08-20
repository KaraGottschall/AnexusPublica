---
title: Convenções
description: Base URL, headers, método QUERY, erros e formatos HTTP da API Anexus
---

# Convenções

Contrato técnico comum a todos os endpoints. Detalhe por recurso: [Referência da API](/desenvolvedores/referencia/).

::: info Status
Autenticação por chave <DevApi field="prefix-family" /> é **prevista**; hoje a área interna usa JWT Bearer. Endpoints e formatos descritos abaixo refletem o backend **entregue**, salvo indicação contrária.
:::

## Base URL

| Ambiente | URL (exemplo) |
|----------|----------------|
| Sandbox | <DevApi field="base-url" env="test" /> |
| Produção | <DevApi field="base-url" env="live" /> |
| Local (dev) | <DevApi field="base-url" env="local" /> |

Todos os paths nesta documentação são relativos a `/api`.

## Autenticação

```http
Authorization: Bearer {token}
```

| Token | Uso |
|-------|-----|
| JWT access token | Área interna (UI) |
| <DevApi field="prefix-wildcard" env="test" /> / <DevApi field="prefix-wildcard" env="live" /> | Integração M2M (**previsto**) |
| (omitido) | Portal anônimo com token de rota, validador público |

## Headers recomendados

| Header | Valor | Obrigatório |
|--------|-------|-------------|
| `Authorization` | `Bearer …` | Endpoints autenticados |
| `Content-Type` | `application/json` | Corpo JSON |
| `Accept-Language` | `pt-BR` | Recomendado (mensagens em português) |

Upload multipart (`attachments`, `validar`): omitir `Content-Type` manual — o cliente define boundary.

Resposta de leituras `QUERY` inclui `Accept-Query: application/json`.

## Método QUERY

Alguns endpoints de **listagem e consulta com filtros** usam o método HTTP **`QUERY`** com corpo JSON — o mesmo padrão da área interna Vue.

```http
QUERY /api/contracts HTTP/1.1
Host: {{api.host.test}}
Authorization: Bearer {{api.key.test.short}}
Content-Type: application/json

{
  "clientName": "Silva",
  "lifecycle": "Active"
}
```

Endpoints que usam `QUERY` hoje:

| Path | Corpo (exemplo) |
|------|-----------------|
| `/api/contracts` | Filtros: `serviceNumber`, `clientName`, `lifecycle`, `expectedDate` |
| `/api/domains/traffic/infractions` | `{ "search": "502" }` |
| `/api/pricing/traffic/quote` | `{ "codigo", "desdobramento", "instance" }` |
| `/api/portal/c/{token}` | `{}` |
| `/api/portal/c/{token}/documents/{documentId}` | `{}` |

Clientes HTTP que não suportam `QUERY` precisam de extensão ou proxy até aliases `POST`/`GET` (**previsto**).

Enums no JSON usam **strings** (ex.: `"Traffic"`, `"DefesaPrevia"`) — `JsonStringEnumConverter` no backend.

## Métodos padrão

| Método | Uso |
|--------|-----|
| `GET` | Detalhe por ID, download de arquivo |
| `POST` | Criação, ações (`pay`, `share-portal`, `close`) |
| `PUT` | Substituição de recurso |
| `PATCH` | Atualização parcial (`beneficiario`) |
| `DELETE` | Remoção (anexo, sessão) |

## Respostas

| Status | Significado |
|--------|-------------|
| `200` | Sucesso com corpo JSON ou arquivo |
| `204` | Sucesso sem corpo |
| `401` | Não autenticado (JWT/chave inválida ou ausente) |
| `403` | Autenticado, sem permissão (tela ou escopo) |
| `404` | Recurso não encontrado (política pode ocultar existência) |
| `409` | Conflito (ex.: e-mail já cadastrado) |
| `422` | Validação de domínio ou documento não reconhecido |
| `429` | Rate limit — ver `Retry-After` |
| `500` | Erro interno |

### Corpo de erro (Problem Details)

```json
{
  "title": "Mensagem legível em português",
  "errors": {
    "ClientEmail": ["E-mail inválido."]
  }
}
```

O frontend prioriza a primeira mensagem em `errors` ou `title`.

## Download de arquivos

Endpoints de download retornam binário com `Content-Disposition`:

- Anexos de contrato: `GET /api/contracts/{id}/attachments/{attachmentId}`
- Relatório LGPD: `GET .../treatment-report`
- Pacote de dados: `GET .../data-package`
- Portal: `QUERY .../portal/c/{token}/documents/{documentId}`

## Versionamento

- Prefixo de path estável: `/api/...`
- OpenAPI: `/openapi/v1.json` (**entregue** em Development; publicação em produção **prevista**)
- Breaking changes: nova versão OpenAPI (`v2`) com período de depreciação documentado

## CORS

SPAs autorizadas listadas em `Cors:Origins`. Integrações **server-side** não dependem de CORS.

## Próximo

- [Superfícies](/desenvolvedores/superficies) — matriz completa de endpoints
- [Primeiros passos](/desenvolvedores/primeiros-passos)
- [Autenticação](/desenvolvedores/autenticacao)

[← Voltar a Desenvolvedores](/desenvolvedores/)
