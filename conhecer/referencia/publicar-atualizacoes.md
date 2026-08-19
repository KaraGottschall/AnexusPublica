---
title: Publicar atualizações
description: Como criar posts da área pública /atualizacoes no aplicativo
---

# Publicar atualizações

A área pública **Atualizações** (`/atualizacoes`) é o changelog da plataforma para visitantes — landing, portal e prospects. Não exige login. O conteúdo vive no repositório [AnexusPublica](https://github.com/KaraGottschall/AnexusPublica), submodule em `frontend/content/anexus-publica/`.

Público e tom: **produto**, o que mudou na experiência. Sem jargão de engenharia. Regras de uso (Guia) e detalhes de implementação (Referência) continuam nestas docs.

## Onde criar o arquivo

Cada post é um arquivo em `atualizacoes/` no repositório **AnexusPublica** (clone em `C:/AnexusPublica` ou via submodule em `frontend/content/anexus-publica/atualizacoes/`).

Convenção de nome: `YYYY-MM-DD-slug.md` — por exemplo, `2026-08-18-cadastro-contratos-em-etapas.md`. O **slug** da URL é o nome do arquivo sem `.md` (`/atualizacoes/2026-08-18-cadastro-contratos-em-etapas`).

**Uma melhoria = um arquivo.** Não agrupe várias entregas no mesmo `.md`; publique cada notícia separadamente, mesmo quando compartilham a mesma data.

O carregador (`frontend/src/lib/atualizacoes.ts`) lê todos os `.md` da pasta, ordena pela data (mais recente primeiro) e expõe lista e detalhe.

## Frontmatter

Obrigatório no topo do arquivo:

```yaml
---
title: Cadastro de contratos em etapas
date: 2026-08-18
summary: Abrir ou editar um contrato na área interna agora segue um assistente claro, passo a passo.
tags:
  - contratos
---
```

| Campo | Uso |
|-------|-----|
| `title` | Título na lista e na página do post |
| `date` | ISO (`YYYY-MM-DD`); ordenação e rótulo “18 de agosto de 2026” |
| `summary` | Uma ou duas frases no card da lista — resume **esta** notícia, não um release inteiro |
| `tags` | Opcional; chips na lista |

O corpo abaixo do frontmatter é Markdown restrito: títulos `##` / `###`, parágrafos, listas, **negrito** e links. HTML cru é escapado.

Links que começam com `/` ou `/referencia/` apontam para o Conhecer em `/conhecer/` (`conhecerUrl`). Não use `localhost` nem tokens de demo no texto.

## Formato jornalístico

Cada melhoria entregue vira **uma notícia** — um arquivo `.md` com o título no frontmatter e subseções fixas no corpo.

```markdown
---
title: Lista de contratos com filtros
date: 2026-08-18
summary: Encontrar um contrato específico na área interna deixou de depender de rolar a tabela inteira.
tags:
  - contratos
---

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

- **Um arquivo = uma melhoria** (ex.: filtros da lista, validador público, recuperação de senha).
- **“Em breve”** também é uma notícia própria — só para itens já visíveis na plataforma (ex. Locação no cadastro).
- O **summary** descreve só aquela notícia; o **title** aparece na lista e no topo da página.
- Traduzir commits de engenharia em benefício de produto (“busca no servidor” em vez de “server-side filtering”).

Exemplo real: [`2026-08-18-cadastro-contratos-em-etapas.md`](https://github.com/KaraGottschall/AnexusPublica/blob/main/atualizacoes/2026-08-18-cadastro-contratos-em-etapas.md).

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

1. Mapear commits do Anexus para notícias (só entregas visíveis ao usuário).
2. Criar **um** `.md` por melhoria em `atualizacoes/` no **AnexusPublica**, com frontmatter e corpo no formato jornalístico.
3. Commit e push no AnexusPublica; atualizar o ponteiro do submodule no monorepo Anexus.
4. Conferir a lista em `/atualizacoes` e o detalhe em `/atualizacoes/{slug}`.
5. Se o item saiu de “previsto”, atualizar [Status de implementação](/referencia/status-implementacao).

O componente `FeatureComingSoon` (Locação no cadastro) aponta para `/atualizacoes`.

## Próximo

- [Status de implementação](/referencia/status-implementacao)
- [Contribuir](/referencia/contribuir)
- [Glossário de produto](/referencia/glossario-produto)
- [Conhecer](/)
