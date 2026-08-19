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

## Pastas aninhadas

Qualquer `.md` em subpastas é descoberto automaticamente (exceto `README.md` e arquivos `_rascunho.md`).

| Seção | Exemplo de arquivo | URL |
|-------|-------------------|-----|
| `atualizacoes/` | `atualizacoes/2026/08/18-portal.md` | `/atualizacoes/2026/08/18-portal` |
| `aprender/` | `aprender/conta/registrar.md` | `/aprender/conta/registrar` |
| `conhecer/` | `conhecer/privacidade/lgpd.md` | `/conhecer/privacidade/lgpd` |

**Conhecer:** páginas novas em subpastas renderizam sem alterar código Vue; adicione entrada na sidebar em `frontend/docs/.vitepress/config.ts` no monorepo Anexus para aparecer no menu.

**Atualizações / Aprender:** frontmatter obrigatório igual aos arquivos na raiz da seção. O slug da URL é o caminho relativo sem `.md`.
