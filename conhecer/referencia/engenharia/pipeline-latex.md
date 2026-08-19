---
title: Pipeline LaTeX
description: Geração de PDF via templates LaTeX e compilação pdfLaTeX
---

# Pipeline LaTeX

A Anexus gera PDFs oficiais compilando templates LaTeX com **pdfLaTeX**. O backend monta um arquivo de dados a partir do contrato e invoca o compilador em diretório temporário.

## Sequência de compilação

1. O montador recebe os dados do contrato, contexto LGPD e prefixo esteganográfico (quando houver).
2. Escolhe o template e gera o arquivo de dados.
3. O compilador copia estilos e arquivos do template, escreve o arquivo de dados em UTF-8 e executa pdfLaTeX **duas vezes** (referências cruzadas, ex.: *Página X de Y* via `lastpage`).
4. Retorna o stream do PDF compilado.

## Seleção de template

O montador decide o template com base no contexto: relatório LGPD se houver contexto LGPD; contrato de locação se o serviço for locação; contrato padrão nos demais casos.

| Template | Arquivo principal | Tipos de serviço |
|----------|-------------------|------------------|
| `lgpd-report` | `main.tex` | Relatório LGPD pós-baixa |
| `locacao` | `contrato-locacao.tex` | Locação veicular |
| `contract` | `main.tex` | Trânsito, Outro, etc. |

## Estrutura dos templates

Cada template contém:

| Arquivo | Papel |
|---------|-------|
| `main.tex` / `contrato-locacao.tex` | Layout — inclui skin e seções |
| `data.example.tex` | Contrato de macros (referência dos campos esperados) |
| `mock-data.tex` | Cenário fictício para compilação local no laboratório |
| `sections/` ou `secoes/` | Blocos modulares do documento |

Há também um diretório compartilhado de estilos (`anexus-base.sty`, `anexus-report.sty`, etc.).

**Regra:** layout e seções não contêm dados de caso hardcoded — tudo vem do arquivo de dados gerado em tempo de execução.

## Pedido de renderização

O montador produz um pedido com quatro elementos:

| Campo | Conteúdo |
|-------|----------|
| TemplateId | Identificador do template (`contract`, `locacao`, `lgpd-report`) |
| DataTex | Conteúdo LaTeX com macros preenchidas |
| MainTexFile | Arquivo principal do template |
| JobName | Nome do job de compilação |

## Compilador pdfLaTeX

O compilador executa os seguintes passos:

1. Cria diretório temporário exclusivo.
2. Copia estilos e arquivos do template (exclui dados de mock e arquivo de dados pré-existente).
3. Escreve o arquivo de dados gerado pelo backend.
4. Executa pdfLaTeX **duas vezes** com modo não interativo e parada em erro.
5. Retorna o stream do PDF e remove o diretório temporário.

O caminho raiz dos templates e o executável pdfLaTeX são configuráveis por ambiente.

## Prefixo esteganográfico

O prefixo esteganográfico é injetado no início dos dados LaTeX:

| Momento | Valor | Motivo |
|---------|-------|--------|
| Registro | ausente | PDF canônico — lacre de conteúdo sem marca de emissão |
| Emissão | string zero-width | Identifica a cópia emitida — ver [Esteganografia](/referencia/engenharia/esteganografia) |

## Escape de caracteres LaTeX

Antes de inserir texto do usuário nas macros, o backend aplica escape TeX. Formalmente, para uma string $s$:

$$\mathcal{E}(s) : \Sigma \to \Sigma^*$$

mapeando caracteres reservados para comandos LaTeX:

| Caractere | Saída TeX |
|-----------|-----------|
| `\` | `\textbackslash\{\}` |
| `\{` `\}` | `\\{` `\\}` |
| `$` `%` `#` `_` | `\$` `\%` `\#` `\_` |
| `&` | `\&` |
| `~` | `\textasciitilde\{\}` |
| `^` | `\textasciicircum\{\}` |

Valores numéricos e datas passam por formatação pt-BR antes do escape.

## Próximo

- [Hasher e lacre](/referencia/engenharia/hasher) — o que acontece com o PDF após a compilação
- [Esteganografia](/referencia/engenharia/esteganografia) — prefixo invisível na emissão
