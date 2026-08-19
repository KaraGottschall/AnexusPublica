---
title: Fixtures de contratos
description: IDs de demo, URLs locais e componentes de preview da área interna de contratos
---

# Fixtures de contratos

Fonte dos dados: `frontend/src/lib/contract-mock-data.ts` (`CONTRACT_DEMO_IDS`, `createInitialContracts`, `getContractDemo`, `getContractDemoList`, `getContractDemoKpis`). Usados pelos componentes de preview do VitePress; a área interna do app consome a API.

## IDs

| ID | Lifecycle | Destaque | Página / seção do Guia |
|----|-----------|----------|------------------------|
| `ct-rascunho-1` | `rascunho` | Pedido ainda não enviado | [Lista e operações](/telas/contratos/lista) |
| `ct-sem-ben` | `documento_gerado` | Sem beneficiário | [Lista e operações](/telas/contratos/lista) |
| `ct-aguardando-1` | `aguardando_aceite` | Fixture legado (badge **Pendente**) | Status e accordion em [Lista](/telas/contratos/lista) |
| `ct-ativo-1` | `ativo` | Etapa `defesa_gerada`, lacrado | Status em [Lista](/telas/contratos/lista) |
| `ct-baixado-1` | `baixado` | Serviço encerrado | Lista (preview completo) |
| `ct-cancelado-1` | `cancelado` | Encerrado sem baixa | Lista (preview completo) |

URL local da tela: `http://localhost:5173/contratos` — [Lista e operações](/telas/contratos/lista).

## Componentes de preview (VitePress)

| Demo | Uso |
|------|-----|
| `<ContractsKpiDemo />` | Só os KPIs (com escala uniforme no viewer) |
| `<ContractsListCadastroDemo />` | Cabeçalho + botão que abre o Dialog de cadastro (sem tabela) |
| `<ContractAccordionDemo contract-id="…" />` | Interior do accordion (detalhes do pedido) |
| `<ContractsListDemo />` | KPIs + tabela completa com fixtures |
| `<ContractFormDemo mode="create" />` | Formulário de cadastro embutido (Dialog sem overlay — não trava a página) |
| `<ContractFormDemo mode="edit" contract-id="…" />` | Formulário de edição com seed |
| `<ContractRowDemo contract-id="…" />` | Uma linha da tabela (status / ações) |
| `<ContractRowDemo contract-id="…" columns="status-actions" />` | Só colunas Status e Ações (badges) |
| `<ContractRowStatusDemo />` | Status e ações com toggle Aguardando aceite / Ativo com etapa |
| `<ContractRowDemo contract-id="…" expanded static-links />` | Linha + accordion aberto |

No Markdown do Guia, o `contract-id="…"` fica só no markup do componente — não no texto visível ao usuário final.

## Próximo

- [Fixtures do portal](/referencia/fixtures-portal)
- [Status de implementação](/referencia/status-implementacao)
- [Contribuir](/referencia/contribuir)
- [Lista e operações](/telas/contratos/lista)
