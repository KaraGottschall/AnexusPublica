---
title: Desenvolvedores
description: Visão da API Anexus — para quem integra, como autenticar, ambientes e o que está disponível
---

# Desenvolvedores

A **API da Anexus** permite que sistemas externos automatizem o que hoje é feito na área interna: abrir pedidos, consultar contratos, anexar documentos, cotar honorários e compartilhar o portal com o beneficiário.

Esta seção é para **quem integra** (ERP, CRM, scripts internos, parceiros). A documentação de produto para o usuário final continua em [Conhecer](/); tutoriais da interface em [/aprender](/aprender). Conteúdo técnico interno do time fica em [Referência](/referencia/).

::: info Status
Parte desta seção descreve o **modelo alvo** da API pública. O que já funciona hoje na aplicação, o que é mock e o que está previsto está em [Status de implementação](/referencia/status-implementacao).
:::

## Para quem é

| Público | Uso típico |
|---------|------------|
| **Escritório / operador** | Integrar o fluxo de contratos ao sistema do escritório |
| **Parceiro técnico** | Construir automações em nome de um tenant |
| **Titular / beneficiário** | **Não** usa API key — acessa o [Portal](/telas/portal/) por link seguro |
| **Público geral** | Validação de integridade documental em `/validar` (sem credencial) |

A API não substitui quem elabora o documento nem o papel da Anexus como operadora — organiza o **pedido**, o **dossiê** e a **transparência** descritos em [Plataforma](/plataforma).

## Como a seção está organizada

### Credenciais

<DocTermList>
  <DocTerm term="Criar chave API" href="/desenvolvedores/criar-chave-api" description="Gerar, usar e revogar chaves do tenant" />
  <DocTerm term="Conexão MCP" href="/desenvolvedores/conexao-mcp" description="Integração via Model Context Protocol (em elaboração)" />
</DocTermList>

### Fundamentos

Política e modelo antes de integrar:

<DocTermList>
  <DocTerm term="Autenticação" href="/desenvolvedores/autenticacao" description="JWT para UI, chaves para M2M, portal e validador público" />
  <DocTerm term="Ambientes" href="/desenvolvedores/ambientes" description="Sandbox vs produção, URLs e isolamento de dados" />
  <DocTerm term="Escopos" href="/desenvolvedores/escopos" description="Escopos explícitos em chaves adicionais; padrão de teste com acesso ilimitado" />
  <DocTerm term="Preços e limites" href="/desenvolvedores/precos-e-limites" description="Honorário vs acesso à API; rate limits" />
</DocTermList>

### Integração

Como chamar a API no dia a dia:

<DocTermList>
  <DocTerm term="Convenções" href="/desenvolvedores/convencoes" description="Base URL, headers, método QUERY, erros" />
  <DocTerm term="Primeiros passos" href="/desenvolvedores/primeiros-passos" description="Tutorial alvo em sandbox" />
  <DocTerm term="Superfícies" href="/desenvolvedores/superficies" description="Matriz endpoint → auth → escopo → status" />
</DocTermList>

### Referência de recursos

Detalhe por área da API (alvo OpenAPI v1):

<DocTermList>
  <DocTerm term="Referência da API" href="/desenvolvedores/referencia/" description="Índice, versionamento e links OpenAPI" />
</DocTermList>

## Domínios

Teoria de negócio (atores, contratos, pedido, assinatura) está em [Domínios](/desenvolvedores/dominios/) — use o menu **Domínios** nesta seção.

## Doc → código

Esta documentação é o **contrato alvo** para implementação no backend. Quando a doc e o app divergirem, [Status de implementação](/referencia/status-implementacao) registra o gap até o código alcançar o alvo.

## Por onde começar

1. [Autenticação](/desenvolvedores/autenticacao) — escolher o mecanismo certo (JWT, chave, portal ou nenhum)
2. [Ambientes](/desenvolvedores/ambientes) — homologar no sandbox antes da produção
3. [Criar chave API](/desenvolvedores/criar-chave-api) — chave de teste padrão (já criada no cadastro) ou credencial adicional
4. [Primeiros passos](/desenvolvedores/primeiros-passos) — fluxo completo no sandbox

## Relacionado

- [Plataforma](/plataforma) — missão e pilares
- [Referência](/referencia/) — engenharia interna e status do app
- [Status de implementação](/referencia/status-implementacao) — entregue vs previsto
