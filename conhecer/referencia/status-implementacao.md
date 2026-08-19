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
| Pedido e contrato | Cadastro, conferência e pagamento | previsto | Cadastro em 4 passos e pagamento interno existem; fase `documento_gerado` e sequência completa descrita em [Contratos](/contratos/) ainda não |
| FAQ | Página pública `/faq` | previsto | Rascunho de perguntas no [Guia — FAQ](/faq); sem rota no app |
| Notificações | E-mail e alertas por etapa | preview/mock | Outbox SQL + Graph OAuth quando configurado; fallback log-only em Development — [Progresso e notificações](/contratos/progresso) |
| Multi-tenant | Contas de organização | previsto | Tenant e membership no backend; sem UI de cadastro ou gestão de organização |
| Assinatura | ICP-Brasil | previsto | Aceite eletrônico interno disponível; ICP em progresso — [Assinatura e integridade](/contratos/assinatura) |
| Domínio | Renomeação `tipoDefesa` → `tipoServico` | previsto | Rótulo de cadastro **Tipo de serviço**; tipos no domínio/API ainda misturam os nomes — [Glossário](/referencia/glossario-produto) |
| Tipo Locação | Pedido, pipeline e honorários | previsto | Opção no cadastro com `FeatureComingSoon`; `ServiceType.Rental` sem pipeline — [Tipos de serviço](/tipos-de-servico/) |
| Integração contábil | Confirmar e pagar | previsto | Lançamento automático ao pagar, se o operador tiver cadastro contábil |
| Portal | Prévia inválida no download | previsto | Antes da baixa, contrato com marca d'água e valores fictícios — [Assinatura](/contratos/assinatura#previa-invalida-e-documento-oficial) |
| Portal / baixa | PDF oficial após baixa | previsto | Documento oficial só após encerramento do serviço (baixa) |
| Área interna | Stripe Checkout (honorários) | entregue | Pagamento único em `/app/contratos/{id}` após a conferência dos termos; webhook confirma e ativa o contrato |
| Notificações | E-mail de portal ao beneficiário | previsto | Após a ativação, envia **link** `/portal/c/{token}` se houver e-mail do beneficiário; PDF oficial só após a baixa; remetente depende de `Email:OAuth:From` |
| LGPD | Relatório de tratamento pós-baixa | preview/mock | PDF via template LaTeX (`TreatmentReport`); requer TeX Live em Development; download na área interna |
| LGPD | ZIP e relatório pós-baixa | preview/mock | ZIP e PDF enviados ao titular e ao controlador via outbox `SendEmail` (Graph ou log-only) |
| LGPD | Pipeline de anonimização pós-entrega | preview/mock | Anonimização real no banco/arquivos; agendada via outbox `ScheduledAt` (`Outbox:AnonymizationRetentionDays`); e-mail ao controlador na execução |
| LGPD | Encaminhamento ao controlador | preview/mock | Solicitação persiste + outbox SQL + Graph ou log-only; inbox em Configurações |
| Referência | Página de API na documentação | previsto | OpenAPI em Development (`/openapi/v1.json`); referência publicada na docs ainda não |

Já entregue (não listado): filtros da lista de contratos (Nº, Cliente, Status, Data prevista); stepper e badges por tipo de serviço (trânsito e outro); cadastro em Dialog com assistente de 4 passos; página de detalhe do contrato; portal read-only do beneficiário; área pública `/atualizacoes` ([Publicar atualizações](/referencia/publicar-atualizacoes)).

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
