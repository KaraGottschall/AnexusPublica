---
title: Hasher e lacre
description: Normalização canônica, SHA-256 por seção, root hash e persistência do lacre documental
---

# Hasher e lacre

O lacre da Anexus **não** é apenas o SHA-256 do arquivo PDF. O sistema extrai o texto de cada **seção semântica**, normaliza o conteúdo de forma determinística, calcula um hash por seção e deriva um **root hash** concatenando os resultados em ordem fixa.

Isso permite detectar adulteração **parcial** — uma cláusula alterada diverge na seção correspondente, mesmo que o restante do documento pareça intacto.

## Pipeline de hash

1. Extrai o texto de cada seção do PDF ($t_1 \ldots t_n$).
2. Aplica normalização canônica $N$ a cada trecho.
3. Calcula SHA-256 em hex para cada seção ($h_1 \ldots h_n$).
4. Concatena os hashes na ordem do catálogo e deriva o root hash $H_{\text{root}}$.
5. Persiste o lacre documental.

## Catálogo de seções

As seções são definidas por template, com catálogo fixo de identificador, rótulo e marcador de extração.

**Contrato** (`contract`):

| ID | Label |
|----|-------|
| `capa` | Capa |
| `partes` | Qualificação das Partes |
| `clausulas` | Cláusulas Principais |
| `assinaturas` | Quadro de Assinaturas |

**Locação** (`locacao`) — 10 seções: quadro-resumo, qualificação, objeto, prazos, financeiro, garantias, rescisão, vistoria, disposições gerais, assinaturas.

**Relatório LGPD** (`lgpd-report`) — 9 seções: capa, resumo, papéis, bases legais, timeline, dossiê, acessos, ciclo de vida, observações.

O extrator de texto usa os marcadores do catálogo para mapear o conteúdo extraído do PDF para cada seção.

## Normalização canônica

Antes de hashear, o texto passa por normalização determinística:

$$N(t) = \text{trim}\big(\text{ws}( \text{NFC}(\text{stripZW}(t)) ) \big)$$

onde:

- $\text{stripZW}$ remove $[\texttt{U+200B}, \texttt{U+200C}, \texttt{U+200D}, \texttt{U+FEFF}]$
- $\text{NFC}$ aplica normalização Unicode Form C
- $\text{ws}$ colapsa sequências de whitespace em um único espaço
- $\text{trim}$ remove espaços nas extremidades

Para payloads JSON (quando aplicável):

$$N_{\text{json}}(o) = \text{serialize}(\text{sortKeys}(o))$$

com chaves ordenadas recursivamente, camelCase, sem indentação e nulls omitidos.

## Hash por seção

Para cada seção $i$ com texto extraído $t_i$:

$$h_i = \text{SHA256}_{\text{hex}}( N(t_i) )$$

O resultado é uma string hexadecimal de **64 caracteres minúsculos**.

Se uma seção não for encontrada no PDF, $t_i = \varepsilon$ (string vazia) — o hash ainda é calculado de forma determinística. Isso ocorre, por exemplo, quando o PDF foi rasterizado e não possui mais camada de texto vetorial — ver [Validação forense — PDF rasterizado](/referencia/engenharia/validacao-forense#pdf-rasterizado).

## Root hash

Os hashes das seções são concatenados **na ordem do catálogo** (não alfabética):

$$H_{\text{root}} = \text{SHA256}_{\text{hex}}( h_1 \Vert h_2 \Vert \cdots \Vert h_n )$$

Ou seja: concatena-se $h_1, h_2, \ldots, h_n$ nessa ordem e aplica-se SHA-256 sobre o resultado.

## Hash binário do PDF

Na **emissão de cópia**, após injeção de metadados XMP, o sistema calcula também:

$$H_{\text{pdf}} = \text{SHA256}_{\text{hex}}( \text{bytes}(\text{PDF}) )$$

Esse valor identifica a **cópia exata** do arquivo emitido.

## $H_{\text{root}} \neq H_{\text{pdf}}$

| Hash | Escopo | Quando | Uso |
|------|--------|--------|-----|
| $H_{\text{root}}$ | Conteúdo semântico por seção | Registro | Lacre canônico — compara seções na validação |
| $H_{\text{pdf}}$ | Bytes do arquivo | Emissão | Impressão digital da cópia específica |

Uma emissão pode ter $H_{\text{pdf}}$ distinto entre cópias (XMP, esteganografia), mas $H_{\text{root}}$ permanece o mesmo se o conteúdo das seções for idêntico após normalização.

## Persistência

O lacre documental armazena:

| Campo | Conteúdo |
|-------|----------|
| ContractId | Referência ao contrato |
| TemplateId | `contract`, `locacao` ou `lgpd-report` |
| SchemaVersion | Versão do esquema de seções |
| RootHash | $H_{\text{root}}$ |
| SectionsJson | Lista serializada de `{ sectionId, label, hash }` |
| RegisteredAt | Timestamp do registro |

O registro ocorre na ativação do contrato ou na geração do relatório LGPD. É idempotente — não sobrescreve registro existente para o mesmo par contrato/template.

## Momento no fluxo

1. Contrato ativado → montagem LaTeX + compilação → PDF canônico
2. Extração por seção → $N(t_i)$ → $h_i$ → $H_{\text{root}}$
3. Persistência do lacre
4. Em emissões posteriores, o validador recalcula $h_i^{\text{sub}}$ e compara com $h_i^{\text{reg}}$

Ver [Validação forense](/referencia/engenharia/validacao-forense) para o fluxo de conferência.

## Próximo

- [Esteganografia](/referencia/engenharia/esteganografia) — por que o payload zero-width não afeta $h_i$
- [Pipeline LaTeX](/referencia/engenharia/pipeline-latex) — origem do PDF hasheado
