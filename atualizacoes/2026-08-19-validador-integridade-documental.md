---
title: Validador público de integridade documental
date: 2026-08-19
summary: Qualquer pessoa pode conferir se um PDF emitido pela Anexus ainda é íntegro — sem login.
tags:
  - validação
  - segurança
---

### O problema antigo

Depois que um contrato ou relatório saía da plataforma, não havia forma pública de verificar se o arquivo foi alterado, reimpresso ou adulterado. A confiança dependia só do visual ou de contato com o escritório.

### A solução

A página **Integridade documental** (`/validar`) recebe o PDF e analisa lacres, hashes por seção e rastreabilidade forense. O resultado mostra se o documento é íntegro, adulterado ou não reconhecido como emitido pela Anexus.

### O que muda

- Validação disponível para visitantes — não exige conta
- Três desfechos claros: íntegro, adulterado, não reconhecido
- Detalhes de proveniência quando o documento é vinculado a um contrato
- Mensagem específica quando o PDF não corresponde a nenhum documento da plataforma

### Saiba mais

- [Validação forense](/referencia/engenharia/validacao-forense)
- [Assinatura e integridade](/dominios/contratos-assinatura)
