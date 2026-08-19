---
title: Fixtures do portal
description: Tokens de demo, URLs locais e componentes de preview do portal
---

# Fixtures do portal

Fonte dos dados: `frontend/src/lib/portal-mock-data.ts` (`DEMO_TOKENS`, `createInitialPortalLinks`, `getPortalDemoLink`).

Em desenvolvimento, a página `/portal` do aplicativo pede o link ou o token. `demo-invalido` e tokens desconhecidos resolvem como `null` em `getPortalDemoLink`.

O portal é **somente leitura** e exclusivo do **beneficiário**. Não há identificação de ator, aceite nem pagamento nessas telas.

## Tokens

| Token | Fase | Flags | URL local | Página do Guia |
|-------|------|-------|-----------|----------------|
| `demo-ativo` | `ativo` | dossiê visível, stepper do serviço | `http://localhost:5173/portal/c/demo-ativo` | [Dossiê](/telas/portal/dossie) |
| `demo-invalido` | — | sempre `null` (404) | `http://localhost:5173/portal/c/demo-invalido` | [Token inválido](/telas/portal/token-invalido) |

Início do portal (sem token): `http://localhost:5173/portal` — [Início](/telas/portal/inicio).

LGPD: `http://localhost:5173/portal/lgpd` — [Privacidade (LGPD)](/telas/portal/lgpd). Contexto legal e canais: [Privacidade de Dados](/privacidade/).

## Componentes de preview (VitePress)

| Demo | Uso |
|------|-----|
| `<PortalHomeDemo />` | `/portal` — card de link/token |
| `<PortalContractDemo token="…" />` | Estados de `/portal/c/{token}` via `getPortalDemoLink` |
| `<PortalContractHeaderDemo />` | Cabeçalho do dossiê (área do beneficiário) |
| `<PortalDossierDemo />` | Card “Documentos do dossiê” |
| `<PortalNotFoundDemo />` | Token inválido |
| `<PortalLgpdDemo />` | `/portal/lgpd` |

No Markdown do Guia, o `token="…"` fica só no markup do componente — não no texto visível ao usuário final.

## Próximo

- [Status de implementação](/referencia/status-implementacao)
- [Contribuir](/referencia/contribuir)
- [Portal](/telas/portal/)
