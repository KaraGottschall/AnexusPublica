# AnexusPublica

Conteúdo editorial da plataforma Anexus — fora do repositório de código (`Anexus`).

## Estrutura

| Pasta | Uso |
|-------|-----|
| `conhecer/` | Documentação pública (VitePress → `/conhecer/`) |
| `atualizacoes/` | Changelog editorial (`/atualizacoes`) |
| `aprender/` | Tutoriais passo a passo (`/aprender`) |
| `artigos/` | Reservado para publicações futuras |

## Convenções

### Atualizações

- Arquivo: `atualizacoes/YYYY-MM-DD-slug.md`
- Frontmatter: `title`, `date`, `summary`, `tags` (opcional)

### Aprender

- Arquivo: `aprender/slug.md`
- Frontmatter: `title`, `description`, `order`, `track`, `duration`

### Conhecer

- Espelha a árvore de URLs em `/conhecer/`
- Assets estáticos em `conhecer/public/`

## Consumo no Anexus

Este repositório é um **submodule** em `frontend/content/anexus-publica/` no monorepo Anexus.

```bash
git clone --recurse-submodules https://github.com/KaraGottschall/Anexus.git
# ou, após clone:
git submodule update --init --recursive
```

Para publicar conteúdo: commit aqui, depois atualize o ponteiro do submodule no Anexus.
