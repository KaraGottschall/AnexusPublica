---
title: Referência — Validação
description: POST /api/validar — integridade forense de PDF público
---

# Referência — Validação

Endpoint público de **validação de integridade documental** — independente de contratos e API keys.

Base: `POST /api/validar`. UI pública: `/validar`. Algoritmo: [Engenharia — Validação forense](/referencia/engenharia/validacao-forense).

## Requisição

```http
POST /api/validar HTTP/1.1
Host: {{api.host.live}}
Content-Type: multipart/form-data

file=@documento.pdf
```

| Restrição | Valor |
|-----------|-------|
| Formato | PDF |
| Tamanho | Limite configurável (`DocumentValidationSettings`) |
| Auth | Nenhuma |

## Resposta

### Sucesso (`200`)

```json
{
  "status": "Integro",
  "sections": [ ... ]
}
```

Status possíveis: `Integro`, `AdulteradoParcialmente`, `TotalmenteInvalido`, `RevogadoPorFraude`, `NaoReconhecido`.

### Documento não reconhecido (`422`)

Corpo inclui `status: "NaoReconhecido"` — tratado como resposta válida na UI pública.

### Rate limit (`429`)

Limite por IP em janela fixa. Header `Retry-After` quando disponível.

| Item | Valor |
|------|-------|
| Status implementação | **entregue** |
| Rate limit | **entregue** |

## Relação com API de integração

| Aspecto | Validador | API contratos |
|---------|-----------|---------------|
| Auth | Anônimo | JWT / chave |
| Cobrança | Gratuito (rate limit) | Honorário por contrato |
| Uso | Público, one-off | B2B operacional |

Uso em **volume alto** por parceiros pode virar produto comercial separado — [Preços e limites](/desenvolvedores/precos-e-limites).

## Próximo

- [Autenticação](/desenvolvedores/autenticacao)
- [Superfícies](/desenvolvedores/superficies)
- [Engenharia — Validação forense](/referencia/engenharia/validacao-forense)

[← Referência da API](/desenvolvedores/referencia/)
