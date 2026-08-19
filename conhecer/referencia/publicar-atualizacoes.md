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
summary: Cadastro em etapas, portal com progresso por tipo de serviço e ciclo de vida dos dados.
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
| `summary` | Uma ou duas frases no card da lista |
| `tags` | Opcional; chips na lista |

O corpo abaixo do frontmatter é Markdown restrito: títulos `##` / `###`, parágrafos, listas, **negrito** e links. HTML cru é escapado.

Links que começam com `/` ou `/referencia/` apontam para o Conhecer em `/conhecer/` (`conhecerUrl`). Não use `localhost` nem tokens de demo no texto.

## Tom

| Canal | Audiência | Conteúdo |
|-------|-----------|----------|
| **Atualizações** (app) | Qualquer visitante | O que melhorou na experiência; “em breve” só para itens já visíveis (ex. Locação) |
| **Conhecer** | Operador, contratante, beneficiário | Porquê e regras do produto |
| **Referência** | Time | Fixtures, status, este workflow |

Não copie páginas do Conhecer para o post: um parágrafo e um link bastam.

## Checklist de um release

1. Criar o `.md` em `atualizacoes/` no **AnexusPublica** com frontmatter válido.
2. Commit e push no AnexusPublica; atualizar o ponteiro do submodule no monorepo Anexus.
3. Conferir a lista em `/atualizacoes` e o detalhe em `/atualizacoes/{slug}`.
4. Se o item saiu de “previsto”, atualizar [Status de implementação](/referencia/status-implementacao).

O componente `FeatureComingSoon` (Locação no cadastro) aponta para `/atualizacoes`.

## Próximo

- [Status de implementação](/referencia/status-implementacao)
- [Contribuir](/referencia/contribuir)
- [Glossário de produto](/referencia/glossario-produto)
- [Conhecer](/)
