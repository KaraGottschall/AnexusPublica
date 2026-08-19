---
title: Criar chave API
description: Como gerar, configurar e revogar chaves de API na Anexus
---

# Criar chave API

As **chaves de API** permitem que aplicações externas se autentiquem na Anexus sem login interativo. Cada chave identifica o operador e define o escopo de acesso aos endpoints.

## Pré-requisitos

- Conta de **operador** com permissão de administrador na área interna
- Ambiente de desenvolvimento ou produção configurado

## Passo a passo

### 1. Acessar as configurações

<!-- TODO: descrever navegação na área interna (menu, rota, permissão) -->

1. Faça login na área interna
2. Acesse **Configurações** → **Chaves de API**
3. Clique em **Nova chave**

### 2. Definir nome e escopo

<!-- TODO: listar escopos disponíveis quando implementados -->

| Campo | Descrição |
|-------|-----------|
| **Nome** | Identificação da chave (ex.: "Integração ERP", "Webhook contratos") |
| **Escopo** | Permissões concedidas à chave |

### 3. Copiar e armazenar a chave

Após a criação, a chave completa é exibida **uma única vez**. Copie e guarde em local seguro — não será possível visualizá-la novamente.

```
<!-- TODO: exemplo de formato da chave -->
anx_live_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

::: warning
Nunca compartilhe chaves em repositórios públicos, logs ou mensagens. Trate-as como senhas.
:::

## Usar a chave nas requisições

Envie a chave no cabeçalho `Authorization` de cada requisição:

```http
GET /api/contratos HTTP/1.1
Host: api.anexus.com.br
Authorization: Bearer anx_live_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

<!-- TODO: confirmar formato exato do header quando a API estiver documentada -->

## Revogar ou rotacionar

Para invalidar uma chave comprometida ou encerrar uma integração:

1. Acesse **Configurações** → **Chaves de API**
2. Localize a chave na lista
3. Clique em **Revogar**

A revogação é imediata — requisições com a chave antiga passam a retornar `401 Unauthorized`.

## Próximo

- [Desenvolvedores — visão geral](/desenvolvedores/)
- [Contratos](/contratos/) — domínio principal da API
- [Status de implementação](/referencia/status-implementacao) — o que já está disponível

[← Voltar a Desenvolvedores](/desenvolvedores/)
