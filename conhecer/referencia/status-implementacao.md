---
title: Status de implementação
description: Checklist do que ainda falta no aplicativo
---

# Status de implementação

Checklist para o time. O [Guia](/) descreve o comportamento de produto; esta página registra o que **ainda não** está completo.

O front consome a API (`/api`) para autenticação, contratos, início, configurações e portal. E-mails transacionais passam pelo outbox SQL (`SendEmail`); o envio real usa Microsoft Graph (`Mail.Send`) quando OAuth está configurado, senão cai em log-only. Solicitações LGPD persistem no banco e são encaminhadas ao controlador pela mesma fila. Itens já entregues nessas áreas não aparecem na tabela abaixo.

| Status | Significado |
|--------|-------------|
| **preview/mock** | Parcial no app ou coberto só por fixtures / demos da documentação |
| **previsto** | Comportamento descrito no Guia; implementação ainda incompleta |

## Checklist

| Área | Item | Status | Notas |
|------|------|--------|-------|
| Documentação | Previews do Guia (contratos e portal) | preview/mock | Demos VitePress ainda usam fixtures locais; o app usa API — ver [Fixtures do portal](/referencia/fixtures-portal) e [Fixtures de contratos](/referencia/fixtures-contratos) |
| Pedido e contrato | Cadastro, conferência e pagamento | previsto | Cadastro em 4 passos e pagamento interno existem; fase `documento_gerado` e sequência completa descrita em [Contratos](/dominios/contratos) ainda não |
| FAQ | Página pública `/faq` | previsto | Rascunho de perguntas no [Guia — FAQ](/faq); sem rota no app |
| Assinatura | ICP-Brasil | previsto | Aceite eletrônico interno disponível; ICP em progresso — [Assinatura e integridade](/dominios/contratos-assinatura) |
| Domínio | Renomeação `tipoDefesa` → `tipoServico` | previsto | Rótulo de cadastro **Tipo de serviço**; tipos no domínio/API ainda misturam os nomes — [Glossário](/referencia/glossario-produto) |
| Tipo Locação | Pedido, pipeline e honorários | previsto | Opção no cadastro com `FeatureComingSoon`; `ServiceType.Rental` sem pipeline — [Tipos de serviço](/tipos-de-servico/) |
| Integração contábil | Confirmar e pagar | previsto | Lançamento automático ao pagar, se o operador tiver cadastro contábil |
| Portal | Prévia inválida no download | previsto | Antes da baixa, contrato com marca d'água e valores fictícios — [Assinatura](/dominios/contratos-assinatura#previa-invalida-e-documento-oficial) |
| Portal / baixa | PDF oficial após baixa | previsto | Documento oficial só após encerramento do serviço (baixa) |
| Notificações | E-mail de portal ao beneficiário | previsto | Após a ativação, envia **link** `/portal/c/{token}` se houver e-mail do beneficiário; PDF oficial só após a baixa; remetente depende de `Email:OAuth:From` |
| Referência | OpenAPI em produção | previsto | Spec em Development (`/openapi/v1.json`); doc alvo em [Desenvolvedores](/desenvolvedores/) |

## API pública {#api-publica}

Checklist derivado de [Desenvolvedores](/desenvolvedores/) — doc-alvo vs código.

| Área | Item | Status | Notas |
|------|------|--------|-------|
| API pública | Entidade `ApiKey` (tenant, hash, prefix, escopos) | previsto | Chave por organização; par teste padrão (público/privado) no cadastro com todos os escopos v1 |
| API pública | Middleware dual auth (JWT + `anx_test_` / `anx_live_`) | previsto | Mesmos handlers MediatR |
| API pública | Policies por escopo (`contracts:read`, …) | previsto | Substituir `screens.*` só na API M2M |
| API pública | Validação chave ↔ ambiente (test só sandbox, live só prod) | previsto | [Ambientes](/desenvolvedores/ambientes) |
| API pública | UI <SettingsPath section="desenvolvedor" item="api-keys" /> (perfil verificado; live só Owner) | previsto | [Criar chave API](/desenvolvedores/criar-chave-api) |
| API pública | Deploy sandbox separado (URL + DB isolado) | previsto | Stripe test, e-mail log-only |
| API pública | Rate limit por chave de API | previsto | Hoje: rate limit em `/validar`, doc-review, password-reset |
| API pública | Aliases GET/POST para endpoints `QUERY` | previsto | [Convenções](/desenvolvedores/convencoes) |
| API pública | Endpoints contratos/precificação via chave | previsto | Endpoints **entregues** com JWT + `screens.contracts` |

Já entregue (não listado): filtros da lista de contratos (Nº, Cliente, Status, Data prevista); stepper e badges por tipo de serviço (trânsito e outro); cadastro em Dialog com assistente de 4 passos; página de detalhe do contrato; portal read-only do beneficiário; área pública `/atualizacoes` ([Publicar atualizações](/referencia/publicar-atualizacoes)); multi-tenant (contas de organização); Stripe Checkout (honorários); e-mail e alertas por etapa; LGPD pós-baixa (relatório, ZIP, anonimização, encaminhamento ao controlador); documentação Desenvolvedores (política + referência).

## Próximo

- [Publicar atualizações](/referencia/publicar-atualizacoes)
- [Fixtures do portal](/referencia/fixtures-portal)
- [Fixtures de contratos](/referencia/fixtures-contratos)
- [Glossário de produto](/referencia/glossario-produto)
- [Parâmetros — precificação trânsito](/referencia/parametros-precificacao-transito)
- [Contribuir](/referencia/contribuir)
- [Guia](/)
- [Plataforma](/plataforma)
- [Precificação](/precificacao/)
- [FAQ](/faq)
