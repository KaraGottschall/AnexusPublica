---
title: Publicar atualizações
description: Como criar posts da área pública /atualizacoes no aplicativo
---

# Publicar atualizações

A área pública **Atualizações** (`/atualizacoes`) é o changelog da plataforma para visitantes — landing, portal e prospects. Não exige login. O conteúdo vive no repositório [AnexusPublica](https://github.com/KaraGottschall/AnexusPublica), submodule em `frontend/content/anexus-publica/`.

Público e tom: **produto**, o que mudou na experiência. Sem jargão de engenharia. Regras de uso (Guia) e detalhes de implementação (Referência) continuam nestas docs.

## Onde criar o arquivo

Cada post é um arquivo em `atualizacoes/` no repositório **AnexusPublica** (clone em `C:/AnexusPublica` ou via submodule em `frontend/content/anexus-publica/atualizacoes/`).

Convenção de nome: `YYYY-MM-DD-slug.md` — por exemplo, `2026-08-18-lancamento-agosto.md`. O **slug** da URL é a parte depois da data (`/atualizacoes/lancamento-agosto`).

O carregador (`frontend/src/lib/atualizacoes.ts`) lê todos os `.md` da pasta, ordena pela data (mais recente primeiro) e expõe lista e detalhe.

## Frontmatter

Obrigatório no topo do arquivo:

```yaml
---
title: Novidades de agosto
date: 2026-08-18
summary: Cadastro guiado em etapas, filtros na lista e progresso no portal por tipo de serviço.
tags:
  - contratos
  - portal
  - privacidade
---
```

| Campo | Uso |
|-------|-----|
| `title` | Título na lista e na página do post |
| `date` | ISO (`YYYY-MM-DD`); ordenação e rótulo “18 de agosto de 2026” |
| `summary` | Uma ou duas frases no card da lista — descreve o release, não lista de bullets |
| `tags` | Opcional; chips na lista |

O corpo abaixo do frontmatter é Markdown restrito: títulos `##` / `###`, parágrafos, listas, **negrito** e links. HTML cru é escapado.

Links que começam com `/` ou `/referencia/` apontam para o Conhecer em `/conhecer/` (`conhecerUrl`). Não use `localhost` nem tokens de demo no texto.

## Formato jornalístico (cards)

Cada melhoria entregue vira um **card** — um bloco `##` com subseções fixas. Não agrupe várias entregas em um parágrafo resumido.

```markdown
## [Título da melhoria — verbo no presente]

[Lead de 1–2 frases: o que mudou e para quem.]

### O problema antigo

[Como era antes — dor concreta do contratante, beneficiário ou operador.]

### A solução

[O que a Anexus passou a fazer — linguagem de produto, sem jargão de commit.]

### O que muda

- [Mudança observável 1]
- [Mudança observável 2]

### Saiba mais

- [Link para Conhecer ou Aprender](/telas/contratos/lista)
```

Regras:

- **Um card = uma melhoria** entregue (ex.: filtros da lista, validador público, recuperação de senha).
- **“Em breve”** fica em card próprio ou seção final — só para itens já visíveis na plataforma (ex. Locação no cadastro).
- O **summary** do frontmatter resume o release inteiro; cada card detalha uma entrega.
- Traduzir commits de engenharia em benefício de produto (“busca no servidor” em vez de “server-side filtering”).

Exemplo real no repositório: [`2026-08-18-lancamento-agosto.md`](https://github.com/KaraGottschall/AnexusPublica/blob/main/atualizacoes/2026-08-18-lancamento-agosto.md).

## Imagens (fase 2)

O renderer atual (`frontend/src/lib/markdown-content.ts`) ainda **não** suporta `![legenda](url)` no corpo nem campo `cover` no frontmatter. Quando o app for atualizado:

- Screenshots WebP por card em `atualizacoes/_assets/` ou subpasta do post
- CSS de card visual em `AtualizacaoDetailView.vue`
- Campo opcional `cover` no frontmatter para imagem de destaque na lista

Até lá, use só texto estruturado nos cards.

## Tom

| Canal | Audiência | Conteúdo |
|-------|-----------|----------|
| **Atualizações** (app) | Qualquer visitante | O que melhorou na experiência; “em breve” só para itens já visíveis (ex. Locação) |
| **Conhecer** | Operador, contratante, beneficiário | Porquê e regras do produto |
| **Referência** | Time | Fixtures, status, este workflow |

Não copie páginas do Conhecer para o post: um parágrafo e um link bastam.

## Checklist de um release

1. Mapear commits do Anexus para cards (só entregas visíveis ao usuário).
2. Criar ou atualizar o `.md` em `atualizacoes/` no **AnexusPublica** com frontmatter e cards no formato jornalístico.
3. Commit e push no AnexusPublica; atualizar o ponteiro do submodule no monorepo Anexus.
4. Conferir a lista em `/atualizacoes` e o detalhe em `/atualizacoes/{slug}`.
5. Se o item saiu de “previsto”, atualizar [Status de implementação](/referencia/status-implementacao).

O componente `FeatureComingSoon` (Locação no cadastro) aponta para `/atualizacoes`.

## Próximo

- [Status de implementação](/referencia/status-implementacao)
- [Contribuir](/referencia/contribuir)
- [Glossário de produto](/referencia/glossario-produto)
- [Conhecer](/)
