# Conhecer (VitePress)

Teoria, regras e contexto do produto em VitePress, servido em `/conhecer/` no mesmo origin do aplicativo.

Este diretório faz parte do repositório [AnexusPublica](https://github.com/KaraGottschall/AnexusPublica). No monorepo Anexus, o caminho é `frontend/content/anexus-publica/conhecer/`.

Tutoriais **Aprender** ficam em `../aprender/`; **Atualizações** em `../atualizacoes/`.

O build gera HTML estático em `frontend/public/conhecer/` no monorepo (gitignorado).

## Desenvolvimento

No monorepo Anexus, pasta `frontend/`:

```bash
pnpm dev        # SPA + Conhecer
pnpm dev:docs   # só VitePress
pnpm build:docs # HTML estático
```

`pnpm dev` sobe o SPA em `http://localhost:5173` e faz proxy de `/conhecer/` para o VitePress.

URLs antigas em `/documentacao/` redirecionam para `/conhecer/`.
