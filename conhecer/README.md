# Conhecer (VitePress)

Teoria, regras e contexto do produto em VitePress, servido em `/conhecer/` no mesmo origin do aplicativo.

Tutoriais passo a passo (**Aprender**) ficam em `frontend/src/content/aprender/` e são servidos pela SPA em `/aprender`.

Fonte: Markdown em `frontend/docs/`. O build gera HTML estático em `frontend/public/conhecer/` (gitignorado).

## Desenvolvimento

```bash
cd frontend
pnpm dev        # SPA + Conhecer
pnpm dev:docs   # só VitePress
pnpm build:docs # HTML estático
```

`pnpm dev` sobe o SPA em `http://localhost:5173` e faz proxy de `/conhecer/` para o VitePress.

URLs antigas em `/documentacao/` redirecionam para `/conhecer/`.
