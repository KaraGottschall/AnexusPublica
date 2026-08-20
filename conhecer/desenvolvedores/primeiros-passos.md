---
title: Primeiros passos
description: Tutorial alvo — integrar no sandbox do zero até share-portal
---

# Primeiros passos

Fluxo recomendado para homologar uma integração no **sandbox** antes de usar chave live.

::: info Status
Passos que dependem de chave <DevApi field="prefix-wildcard" env="test" /> ou UI de Chaves de API estão marcados como **previsto**. A chave de teste padrão (par público/privado no cadastro) é o modelo alvo — endpoints de contrato e precificação já existem com JWT para validar payloads enquanto o auth M2M não está pronto.
:::

## Pré-requisitos

- Conta com **perfil verificado** na Anexus (ou credenciais de homologação fornecidas pelo time)
- [Ambiente sandbox](/desenvolvedores/ambientes) acessível
- Cliente HTTP (curl, Postman, script) com suporte ao método **`QUERY`**

## 1. Obter chave de teste

Cada tenant já tem uma **chave de teste padrão** com acesso ilimitado (todos os escopos v1). Não é preciso criar chave nem marcar escopos para começar.

1. Login na área interna (sandbox)
2. Acesse <SettingsPath section="desenvolvedor" item="api-keys" />
3. Copie o **segredo privado** em <SettingsPath section="desenvolvedor" item="api-keys" /> (mostrar/ocultar ou regenerar quando necessário)
4. Detalhes: [Criar chave API](/desenvolvedores/criar-chave-api#chave-de-teste-padrao-automatica)

Exporte em variável de ambiente:

```bash
export ANEXUS_API_KEY="{{api.key.test.short}}"
export ANEXUS_BASE="{{api.base-url.test}}"
```

## 2. Listar tipos de serviço

Confirma conectividade e escopo `domains:read`.

```http
GET /api/domains/service-types HTTP/1.1
Host: {{api.host.test}}
Authorization: Bearer {{api.key.test.short}}
Accept-Language: pt-BR
```

Resposta esperada: lista com `Traffic`, `Other` (e tipos futuros).

## 3. Cotar honorários (trânsito)

Escopo `pricing:read`. Corpo conforme [Precificação trânsito](/precificacao/transito).

```http
QUERY /api/pricing/traffic/quote HTTP/1.1
Host: {{api.host.test}}
Authorization: Bearer {{api.key.test.short}}
Content-Type: application/json

{
  "codigo": "502-0",
  "desdobramento": 0,
  "instance": "DefesaPrevia"
}
```

Campos de resposta: `fees`, `valorBaseGravidade`, `ready`.

Busca de infrações (autocomplete):

```http
QUERY /api/domains/traffic/infractions HTTP/1.1
Authorization: Bearer {{api.key.test.short}}
Content-Type: application/json

{ "search": "502" }
```

## 4. Criar contrato

Escopo `contracts:write`. Estrutura alinhada a [Pedido e valores](/dominios/contratos-pedido).

```http
POST /api/contracts HTTP/1.1
Host: {{api.host.test}}
Authorization: Bearer {{api.key.test.short}}
Content-Type: application/json

{
  "clientName": "Maria Exemplo",
  "clientDocument": "52998224725",
  "clientEmail": "maria@exemplo.test",
  "expectedDate": "2026-09-30",
  "serviceType": "Traffic",
  "beneficiaryName": "Maria Exemplo",
  "beneficiaryDocument": "52998224725",
  "beneficiaryEmail": "beneficiario@exemplo.test",
  "traffic": {
    "infractionCode": "502-0",
    "desdobramento": 0,
    "instance": "DefesaPrevia",
    "issuingAuthority": "DetranSP"
  }
}
```

Guarde o `id` retornado.

::: tip
CPF/CNPJ devem ser válidos — o backend valida dígitos verificadores.
:::

## 5. Anexar documento

Escopo `contracts:attachments`. Multipart:

```bash
curl -X POST "$ANEXUS_BASE/contracts/{id}/attachments" \
  -H "Authorization: Bearer $ANEXUS_API_KEY" \
  -H "Accept-Language: pt-BR" \
  -F "type=Ait" \
  -F "file=@/caminho/auto.pdf"
```

Tipos de anexo permitidos dependem do `serviceType` — regra igual à UI.

## 6. Compartilhar portal

Escopo `contracts:portal`. Gera token para link do beneficiário.

```http
POST /api/contracts/{id}/share-portal HTTP/1.1
Host: {{api.host.test}}
Authorization: Bearer {{api.key.test.short}}
Content-Type: application/json

{}
```

Use o token retornado (campo do contrato / resposta) para montar:

`{{api.portal-base.test}}/portal/c/{token}`

O beneficiário consulta **sem** API key — [Portal](/telas/portal/).

## 7. (Opcional) Pagamento no sandbox

Escopo `contracts:pay`. Após conferência dos termos na UI ou fluxo equivalente:

```http
POST /api/contracts/{id}/pay HTTP/1.1
Authorization: Bearer {{api.key.test.short}}
Content-Type: application/json

{ "deviceLocation": null }
```

Resposta: `clientSecret`, `publishableKey` para Stripe **test**. Confirmação via webhook — [Ambientes](/desenvolvedores/ambientes).

## 8. Ir para produção

1. Homologar todos os passos acima no sandbox
2. Criar chave <DevApi field="prefix-wildcard" env="live" /> com mesmos escopos necessários (perfil **Owner**)
3. Trocar `ANEXUS_BASE` e credenciais Stripe
4. Revogar chaves de teste não utilizadas

## Enquanto M2M não estiver pronto

Para testar payloads **hoje**:

1. `POST /api/auth/login` com usuário Operator/Owner
2. Usar JWT Bearer nos mesmos endpoints
3. Comparar respostas com a UI em `/app/contratos`

Quando <DevApi field="prefix-wildcard" env="test" /> estiver disponível, substituir apenas o header `Authorization`.

## Próximo

- [Superfícies](/desenvolvedores/superficies)
- [Referência — Contratos](/desenvolvedores/referencia/contratos)
- [Preços e limites](/desenvolvedores/precos-e-limites)

[← Voltar a Desenvolvedores](/desenvolvedores/)
