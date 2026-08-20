---
title: Criar chave API
description: Como gerar, configurar, usar e revogar chaves de API do tenant na Anexus
---

# Criar chave API

As **chaves de API** permitem que aplicações backend se autentiquem na Anexus sem login interativo. Cada chave identifica a **organização (tenant)**.

Chaves **adicionais** podem restringir [escopos](/desenvolvedores/escopos). A **chave de teste padrão** do tenant já vem com **acesso ilimitado** (todos os escopos v1) — sem precisar marcar permissões na criação.

::: info Status
Entidade `ApiKey`, UI em Configurações e middleware de autenticação dual (JWT + chave) são **previstos**. Veja [Status de implementação](/referencia/status-implementacao).
:::

## Pré-requisitos

- Conta na área interna com **perfil verificado** e acesso a **Configurações**
- Perfil **Owner** para criar ou revogar chaves de **produção** (<DevApi field="prefix-wildcard" env="live" />); demais usuários com acesso a Configurações podem criar e gerenciar chaves de **teste**
- [Ambiente](/desenvolvedores/ambientes) correto: sandbox para <DevApi field="prefix-wildcard" env="test" />, produção para <DevApi field="prefix-wildcard" env="live" />

## Chave de teste padrão (automática)

Ao criar a conta (tenant), a Anexus provisiona **um par de chaves de teste** para homologação:

| Parte | O que é | Visibilidade |
|-------|---------|--------------|
| **Identificador (público)** | Prefixo da chave (<DevApi field="prefix-display" env="test" />) | Sempre visível na listagem |
| **Segredo (privado)** | Token completo (<DevApi field="prefix-wildcard" env="test" />) | Exibido e ocultado na seção Desenvolvedores; pode ser **regenerado** |

Propriedades da chave padrão:

- Ambiente **teste** (<DevApi field="prefix-wildcard" env="test" />) — só no sandbox
- **Acesso ilimitado**: todos os escopos v1 concedidos automaticamente — não há etapa de seleção de escopos
- Nome fixo na listagem (ex.: **Chave de teste padrão**)
- **Não revogável** — use **Regenerar** para rotacionar o segredo; a chave antiga invalida imediatamente

Com o segredo em variável de ambiente, você já pode seguir [Primeiros passos](/desenvolvedores/primeiros-passos) sem clicar em **Nova chave**.

::: tip
O segredo pode ser mostrado ou ocultado quantas vezes quiser em <SettingsPath section="desenvolvedor" item="api-keys" />. Se precisar de outra credencial de homologação em paralelo, crie uma chave adicional de teste.
:::

## Criar chave adicional (opcional)

Use **Nova chave** quando precisar de outra credencial — por exemplo, escopos mínimos para um ERP, chave de produção ou rotação sem afetar a padrão.

### 1. Acessar as configurações

1. Faça login na área interna
2. Acesse <SettingsPath section="desenvolvedor" item="api-keys" />
3. Clique em **Nova chave**

### 2. Definir nome, ambiente e escopos

<DocTermList>
  <DocTerm term="Nome" description='Identificação da chave (ex.: "Integração ERP homologação", "Produção CRM")' />
  <DocTerm term="Ambiente" description="Teste ({{api.prefix.test}}) ou produção ({{api.prefix.live}})" />
  <DocTerm term="Escopos" description="Permissões concedidas — ver catálogo em Escopos" />
</DocTermList>

**Recomendações** (chaves adicionais — a padrão de teste já cobre homologação completa):

- Homologação adicional: use escopos mínimos se a integração não precisa de tudo
- Produção: somente **Owner** cria <DevApi field="prefix-wildcard" env="live" /> — após fluxo validado no sandbox
- Chave live exige confirmação explícita de que acessará **dados reais**

### 3. Copiar e armazenar a chave

Após a criação, a chave completa é exibida **uma única vez**. Copie e guarde em cofre de segredos (1Password, Azure Key Vault, etc.) — não será possível visualizá-la novamente.

```
{{api.key.test.sample}}   (sandbox)
{{api.key.live.sample}}   (produção)
```

Na listagem, apenas o **prefixo** permanece visível (ex.: <DevApi field="prefix-display" env="live" />) para identificar a chave.

::: warning
Nunca compartilhe chaves em repositórios públicos, logs, tickets ou mensagens. Trate-as como senhas.
:::

## Usar a chave nas requisições

Envie a chave no cabeçalho `Authorization` de cada requisição à API de integração:

```http
QUERY /api/contracts HTTP/1.1
Host: {{api.host.test}}
Authorization: Bearer {{api.key.test.sample}}
Content-Type: application/json
Accept-Language: pt-BR

{}
```

Convenções completas: [Convenções](/desenvolvedores/convencoes).

## Auditoria

Cada chave registra:

- **Tenant** proprietário
- **Usuário** que criou (`created_by`)
- **Data** de criação e último uso
- **Revogação** (quem e quando)

Revogar a chave de um ex-funcionário **não** exige resetar senhas de login — credenciais M2M são independentes do JWT.

## Revogar ou rotacionar

### Revogação

1. Acesse <SettingsPath section="desenvolvedor" item="api-keys" />
2. Localize a chave **adicional** na lista (a chave de teste padrão não pode ser revogada)
3. Clique em **Revogar** — chaves de **produção** exigem perfil **Owner**

Efeito **imediato** — requisições com a chave antiga retornam `401 Unauthorized`.

### Rotação (recomendado)

1. Crie nova chave com os mesmos escopos
2. Atualize a integração (ERP, CI, variáveis de ambiente)
3. Valide tráfego na nova chave
4. Revogue a chave antiga

Rotacionar periodicamente (ex.: anual) ou imediatamente se houver suspeita de vazamento.

## Próximo

- [Autenticação](/desenvolvedores/autenticacao)
- [Primeiros passos](/desenvolvedores/primeiros-passos)
- [Escopos](/desenvolvedores/escopos)

[← Voltar a Desenvolvedores](/desenvolvedores/)
