---
title: Contribuir
description: Como editar e pré-visualizar o Conhecer (VitePress)
---

# Contribuir

O **Conhecer** fica em Markdown em `frontend/docs/`. O site é gerado com VitePress e publicado em `/conhecer/` no mesmo origin do aplicativo. Tutoriais práticos (**Aprender**) ficam em `frontend/src/content/aprender/` e são servidos pela SPA em `/aprender`.

## Scripts

Na pasta `frontend/`:

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
| `frontend/docs/` | Conhecer — teoria e regras (usuário final) |
| `frontend/docs/referencia/` | Conteúdo técnico e de contribuição |
| `frontend/src/content/aprender/` | Tutoriais Aprender (passo a passo) |
| `frontend/docs/.vitepress/config.ts` | Título, nav, sidebar, `base` e busca local |
| `frontend/docs/.vitepress/theme/` | Tema, diagramas e previews de tela |
| `frontend/public/conhecer/` | HTML gerado pelo build (não versionar) |

Páginas novas precisam de um arquivo `.md` **e** de uma entrada na sidebar em `.vitepress/config.ts` (e em `nav` se for seção de topo).

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

## Anotar na revisão (dev)

Com `pnpm dev`, **clique direito** em qualquer tela do aplicativo ou do Conhecer para abrir o menu **Anotar**. Se o clique for dentro de uma seção (`##` / `###`) ou em um preview/vídeo com `id`, o bloco já vem **pré-selecionado** no modal. Escreva a nota e clique em **Abrir issue no GitHub** — abre uma issue pré-preenchida no repositório `KaraGottschall/Anexus` (label `documentation` nas páginas de docs). Só no servidor de desenvolvimento; o menu nativo do browser é suprimido na área anotável.

## Próximo

- [Glossário de produto](/referencia/glossario-produto)
- [Fixtures do portal](/referencia/fixtures-portal)
- [Fixtures de contratos](/referencia/fixtures-contratos)
- [Publicar atualizações](/referencia/publicar-atualizacoes)
- [Status de implementação](/referencia/status-implementacao)
- [Conhecer](/)
