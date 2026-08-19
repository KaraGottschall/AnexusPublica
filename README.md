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

- Arquivo: `atualizacoes/YYYY-MM-DD-slug.md` — **uma notícia por arquivo** (uma melhoria = um `.md`)
- Frontmatter: `title`, `date`, `summary`, `tags` (opcional)
- Formato: matéria jornalística com subseções fixas no corpo (sem parágrafo introdutório — o `summary` já aparece como subtítulo na página):
  - `### O problema antigo`
  - `### A solução`
  - `### O que muda`
  - `### Saiba mais`
- O `title` do frontmatter é o título na lista; não repita como `##` no corpo
- Várias entregas no mesmo dia = vários arquivos com a mesma data e slugs diferentes
- Imagens no corpo ou capa: fase 2 (requer mudanças no renderer do app Anexus)

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
