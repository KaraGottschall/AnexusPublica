---
title: Contribuir
description: Como editar e pré-visualizar o Conhecer (VitePress)
---

# Contribuir

O conteúdo editorial vive no repositório [AnexusPublica](https://github.com/KaraGottschall/AnexusPublica) (submodule em `frontend/content/anexus-publica/`). O **Conhecer** é gerado com VitePress e publicado em `/conhecer/`. Tutoriais **Aprender** e posts de **Atualizações** são servidos pela SPA em `/aprender` e `/atualizacoes`.

Para escrever conteúdo, abra o repositório AnexusPublica (clone em `C:/AnexusPublica` ou edite via `frontend/content/anexus-publica/` no monorepo).

## Scripts

Na pasta `frontend/` do monorepo Anexus:

```bash
pnpm install
pnpm dev          # SPA + Conhecer (proxy em /conhecer/)
pnpm dev:docs     # só VitePress na porta 5174
pnpm build        # Conhecer estático + SPA
pnpm build:docs   # só o HTML em public/conhecer/
```

O `pnpm dev` sobe o aplicativo em `http://localhost:5173` e o VitePress internamente na porta 5174. Abra o Conhecer em `http://localhost:5173/conhecer/`. URLs antigas em `/documentacao/` redirecionam para `/conhecer/`.

Os previews de tela importam componentes de `frontend/src`. O VitePress libera essa pasta em `server.fs.allow` — sem isso, o browser recebe **403** em URLs `/@fs/...`.

## Estrutura

| Pasta / arquivo | Conteúdo |
|-----------------|----------|
| `frontend/content/anexus-publica/conhecer/` | Conhecer — teoria e regras (Markdown) |
| `frontend/content/anexus-publica/aprender/` | Tutoriais Aprender (passo a passo) |
| `frontend/content/anexus-publica/atualizacoes/` | Posts públicos `/atualizacoes` |
| `frontend/content/anexus-publica/artigos/` | Reservado para publicações futuras |
| `frontend/docs/.vitepress/config.ts` | Título, nav, sidebar, `base` e busca local |
| `frontend/docs/.vitepress/theme/` | Tema, diagramas e previews de tela |
| `frontend/public/conhecer/` | HTML gerado pelo build (não versionar) |

Páginas novas do Conhecer precisam de um arquivo `.md` em `conhecer/` **e** de uma entrada na sidebar em `.vitepress/config.ts`.

## Convenções

- Idioma: PT-BR.
- Nomes de arquivo em kebab-case (`plataforma.md`).
- Um título `#` por página; seções com `##` / `###`.
- Frontmatter obrigatório: `title` e `description`.
- Links internos: caminhos VitePress (`/plataforma`). No app, isso vira `/conhecer/plataforma`.
- **Conhecer**: linguagem teórica — sem localhost, tokens `demo-*`, stack ou status de protótipo no texto.
- **Aprender**: imperativo, passo a passo — tudo que é fazível no produto.
- **Referência**: fixtures, glossário, status de implementação e instruções de contribuição.

Detalhes de diagramas e previews: skill `anexus-docs` no repositório, [Glossário de produto](/referencia/glossario-produto), [Fixtures do portal](/referencia/fixtures-portal) e [Fixtures de contratos](/referencia/fixtures-contratos).

## Publicar conteúdo

1. Commit e push no repositório **AnexusPublica**.
2. No monorepo Anexus: `cd frontend/content/anexus-publica && git pull` e commit do ponteiro do submodule.

## Anotar na revisão (dev)

Com `pnpm dev`, **clique direito** em qualquer tela do aplicativo ou do Conhecer para abrir o menu **Anotar**. Se o clique for dentro de uma seção (`##` / `###`) ou em um preview/vídeo com `id`, o bloco já vem **pré-selecionado** no modal. Escreva a nota e clique em **Abrir issue no GitHub** — abre uma issue pré-preenchida no repositório `KaraGottschall/Anexus` (label `documentation` nas páginas de docs). Só no servidor de desenvolvimento; o menu nativo do browser é suprimido na área anotável.

## Próximo

- [Glossário de produto](/referencia/glossario-produto)
- [Fixtures do portal](/referencia/fixtures-portal)
- [Fixtures de contratos](/referencia/fixtures-contratos)
- [Publicar atualizações](/referencia/publicar-atualizacoes)
- [Status de implementação](/referencia/status-implementacao)
- [Conhecer](/)
