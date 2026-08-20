---
title: Escopos
description: Catálogo de permissões v1 para chaves de API — o que cada escopo permite
---

# Escopos

Chaves **adicionais** recebem **escopos explícitos** — permissões granulares independentes das telas da interface.

A **chave de teste padrão** do tenant (criada automaticamente no cadastro) já inclui **todos os escopos v1** — acesso ilimitado no sandbox, sem etapa de seleção.

::: info Status
Autorização por escopo na API é **prevista**. Hoje a área interna usa políticas de tela (`screens.home`, `screens.contracts`, `screens.settings`) ligadas ao perfil JWT (`Owner`, `Operator`, `Billing`).
:::

## Por que escopos

| Abordagem UI (hoje) | Abordagem API (alvo) |
|---------------------|----------------------|
| Perfil → telas permitidas | Chave → escopos concedidos |
| Operator sem Settings | Chave só com `contracts:read` se desejado |
| Billing sem Contratos | Não se aplica à API pública v1 |

Integradores precisam do **mínimo necessário** (princípio do menor privilégio). Uma chave de leitura para BI não deve criar contratos.

## Catálogo v1

| Escopo | Permite | Endpoints principais |
|--------|---------|----------------------|
| `contracts:read` | Listar e consultar contratos | `QUERY /api/contracts`, `GET /api/contracts/{id}` |
| `contracts:write` | Criar, editar, cancelar, encerrar | `POST`, `PUT`, `PATCH .../beneficiario`, `POST .../close`, `POST .../cancel` |
| `contracts:attachments` | Anexos do contrato | `POST/GET/DELETE .../attachments` |
| `contracts:portal` | Gerar link do portal | `POST .../share-portal` |
| `contracts:pay` | Iniciar pagamento de honorários | `POST .../pay` |
| `pricing:read` | Cotação e infrações de trânsito | `QUERY /api/pricing/traffic/quote`, `QUERY /api/domains/traffic/infractions` |
| `domains:read` | Tipos de serviço | `GET /api/domains/service-types` |

Referência detalhada: [Superfícies](/desenvolvedores/superficies) e [Referência — Contratos](/desenvolvedores/referencia/contratos).

## Combinações típicas

| Caso de uso | Escopos sugeridos |
|-------------|-------------------|
| Dashboard read-only | `contracts:read` |
| ERP — abrir pedido completo | `contracts:read`, `contracts:write`, `contracts:attachments`, `pricing:read`, `domains:read` |
| ERP — enviar portal ao cliente | acima + `contracts:portal` |
| Checkout automatizado | acima + `contracts:pay` |
| Calculadora externa de honorários | `pricing:read`, `domains:read` |

## Equivalência aproximada com perfis da UI

| Perfil UI | Telas | Escopos API típicos (se todos concedidos) |
|-----------|-------|---------------------------------------------|
| **Owner** | Home, Contratos, Settings | Todos os escopos v1 de contratos + pricing + domains |
| **Operator** | Home, Contratos | `contracts:*`, `pricing:read`, `domains:read` |
| **Billing** | Home, Settings | **Sem** escopos de contrato na API pública v1 |

A API **não espelha** perfis automaticamente — quem cria uma chave **adicional** escolhe os escopos. A chave padrão de teste é exceção: todos os escopos v1 já concedidos.

## Fora do v1 público

Estes recursos permanecem **somente JWT / área interna** na primeira versão da API pública:

| Recurso | Motivo |
|---------|--------|
| `GET /api/home/summary` | Agregado de dashboard, não recurso de domínio |
| `GET/PATCH /api/settings` | Preferências do operador |
| `GET /api/lgpd/requests` | Inbox administrativa LGPD |
| `POST /api/doc-review/issues` | Feedback interno de documentação |
| Endpoints demo LGPD (`data-lifecycle/*`, `demo/lgpd-reset`) | Apenas Development/Testing |

Escopos futuros possíveis (não comprometidos): `admin:lgpd`, `webhooks:manage`.

## Respostas de autorização

| Código | Situação |
|--------|----------|
| `401` | Chave ausente, inválida, revogada ou ambiente incorreto |
| `403` | Chave válida, escopo insuficiente para o endpoint |

## Próximo

- [Criar chave API](/desenvolvedores/criar-chave-api) — chave padrão de teste (ilimitada) ou escopos em chaves adicionais
- [Preços e limites](/desenvolvedores/precos-e-limites)
- [Superfícies](/desenvolvedores/superficies)

[← Voltar a Desenvolvedores](/desenvolvedores/)
