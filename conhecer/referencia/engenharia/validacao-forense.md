---
title: Validação forense
description: Endpoint POST /api/validar, três cenários de parecer (íntegro, não reconhecido, adulterado parcialmente) e verificação por seção
---

# Validação forense

A plataforma expõe um endpoint público que recebe um PDF e retorna um **parecer técnico de integridade** — comparando o arquivo submetido com o registro canônico e, quando possível, com a emissão original.

Complementa a conferência manual descrita em [Assinatura — Conferir integridade](/contratos/assinatura#conferir-a-integridade-do-contrato).

## Três cenários de parecer

Na prática, quase todo upload cai em um destes três resultados. Eles correspondem a **perguntas diferentes** — e a Anexus responde cada uma com margem de segurança distinta.

| # | Pergunta que o sistema responde | Status | HTTP |
|---|----------------------------------|--------|------|
| 1 | *“O que saiu da plataforma é o que entrou agora?”* | **Íntegro** | 200 |
| 2 | *“Não consigo afirmar que este PDF é meu — pode estar corrompido, editado por terceiros ou nunca ter sido emitido aqui.”* | **Documento não reconhecido** | 422 |
| 3 | *“Reconheço a emissão, mas parte do conteúdo diverge do lacre — há indícios técnicos fortes de adulteração pós-download.”* | **Adulterado parcialmente** | 200 |

::: warning Limites do parecer
Todos os resultados são **estritamente técnicos**. A Anexus **não** atesta veracidade jurídica, **não** identifica o autor da alteração e **não** substitui perícia judicial. O objetivo é orientar custódia e próximos passos — não “colocar a mão no fogo” sobre fatos que só uma perícia pode confirmar.
:::

---

### Cenário 1 — Documento autêntico (íntegro)

**O que significa:** a cópia analisada corresponde, byte a byte e seção a seção, ao registro canônico lacrado na celebração **e** ao hash binário da emissão original.

**Quando ocorre:** PDF baixado diretamente do portal ou de Minha área, sem reprocessamento, sem edição e sem corrupção no transporte.

**O que a Anexus afirma com relativa segurança:**

- Este arquivo é uma **emissão reconhecida** do contrato vinculado.
- Nenhuma seção do catálogo diverge do lacre.
- A correspondência binária com a emissão registrada foi **confirmada**.

**O que a Anexus não afirma:** que o conteúdo jurídico seja favorável a alguma parte, que assinaturas manuscritas existam fora do PDF, ou que o contrato esteja “válido” no sentido processual — apenas que **a via digital não foi alterada** desde a emissão.

<ValidationIntegroDemo />

---

### Cenário 2 — Documento não reconhecido

**O que significa:** o validador **não conseguiu associar** o PDF a nenhum contrato da plataforma — nem por metadados XMP, nem por esteganografia, nem por padrão de número do contrato/serviço, ou porque não há lacre documental no banco.

**Quando ocorre (exemplos comuns):**

- PDF gerado **fora** da Anexus.
- Arquivo **re-salvo** ou editado em software de terceiros (Acrobat, conversores, “comprimir PDF”, anotações).
- **Corrupção acidental** no envio, download ou armazenamento.
- Edição consensual entre partes **fora** da plataforma — mesmo que o texto pareça “o mesmo contrato”.

**O que a Anexus afirma com relativa segurança:**

- **Não** é possível tratar este arquivo como emissão verificável da plataforma.
- **Não** há base técnica para comparar seções nem emitir parecer de adulteração parcial.

**O que a Anexus não afirma:**

- Que o documento seja **falso** ou **fraudulento** — apenas que **não é reconhecível** como emissão Anexus.
- Que tenha havido **adulteração intencional** — a causa pode ser corrupção, reprocessamento benigno ou arquivo nunca emitido aqui.

Por isso a UI evita linguagem acusatória e orienta a obter uma **nova via diretamente na plataforma**.

<ValidationUnrecognizedDemo />

**Resposta HTTP:** `422 Unprocessable Entity`, corpo com `status: "NaoReconhecido"` (a UI trata como parecer informativo, não como erro genérico de rede).

---

### Cenário 3 — Adulterado parcialmente

**O que significa:** o PDF **passou pela porta de identidade** (XMP, esteganografia ou número do contrato) **e** o lacre por seção detectou divergência em **parte** do conteúdo — com **pelo menos uma seção ainda correspondente**.

**Quando ocorre:** adulteração **cirúrgica pós-emissão** sobre uma cópia legítima — por exemplo, alterar apenas vigência ou prazo nos content streams, **sem** destruir metadados Anexus nem reescrever o arquivo inteiro.

::: info Quem consegue produzir este cenário?
Não exige “hacker de elite”, mas exige **preservar a identidade técnica da emissão** — o oposto de editar visualmente no Acrobat. Edições grosseiras caem no **cenário 2** (422). Adulteração que destrói **todas** as seções tende a **Totalmente inválido** (200), não parcial.
:::

**O que a Anexus afirma com relativa segurança:**

- O arquivo **pertence ao universo** de emissões do contrato identificado (via XMP ou fallback).
- **Seções específicas** divergem do lacre canônico registrado na celebração — com sub-hashes exibidos na auditoria.
- A narrativa de custódia indica que as inconsistências **provavelmente** foram introduzidas **após** a expedição da cópia digital ao signatário rastreado — hipótese técnica, não conclusão penal.

**O que a Anexus não afirma:**

- **Quem** alterou o arquivo.
- **Com que intenção** (erro de digitação vs. fraude).
- Que o documento seja **inexecutável** ou **nulo** juridicamente.

**Recomendação prudente (já presente no parecer):** neste cenário, **análise pericial complementar deve ser fortemente considerada** antes de decisões relevantes. O status `AdulteradoParcialmente` é um **alerta forense técnico** — indício consistente de alteração localizada, não sentença.

<ValidationAdulteradoDemo />

---

## Árvore de decisão (completa)

<ValidationDecisionFlow />

Outros status possíveis (menos frequentes na documentação de produto):

| Status | Condição |
|--------|----------|
| **Totalmente inválido** | Todas as seções divergem, ou conteúdo bate mas hash binário não (ex.: PDF regravado mantendo texto) |
| **Revogado por fraude** | Contrato anonimizado — ciclo de vida encerrado |

### PDF rasterizado

Se um PDF for convertido em imagem e reempacotado sem camada de texto, a extração retorna seções vazias → em geral **Totalmente inválido** (não parcial). Ver nota técnica abaixo.

---

## Endpoint

| Aspecto | Valor |
|---------|-------|
| Método e rota | `POST /api/validar` |
| Content-Type | `multipart/form-data` |
| Campo | `file` (PDF, máx. 20 MB) |
| Autenticação | nenhuma (público) |
| Rate limit | 10 req/min |

| HTTP | Condição |
|------|----------|
| 200 | PDF reconhecido (íntegro, adulterado parcial/total ou revogado) |
| 422 | Documento não reconhecido (`NaoReconhecido`) |
| 429 | Rate limit excedido |

## Fluxo técnico

1. **Hash binário** — $H_{\text{pdf}}^{\text{sub}} = \text{SHA256}_{\text{hex}}(\text{bytes})$ do PDF recebido.
2. **Resolução do contrato** — XMP Anexus → esteganografia zero-width → padrão `Número do contrato | YYYY-NNNNN`.
3. **Lacre documental** — busca `ContractDocumentIntegrity` por contrato e template.
4. **Emissão** — decodifica stego ou busca `DocumentEmission` por hash binário (quando resolução via XMP).
5. **Re-hash por seção** — extrai texto, normaliza, calcula $h_i^{\text{sub}}$ e $H_{\text{root}}^{\text{rec}}$.
6. **Parecer** — status global, auditoria seção a seção, proveniência, narrativa de custódia.

## Verificação por seção

Para cada seção $i$ do catálogo (contrato padrão: Capa, Qualificação das Partes, Cláusulas Principais, Quadro de Assinaturas):

$$\text{status}_i = \begin{cases} \text{Correspondente} & \text{se } h_i^{\text{sub}} = h_i^{\text{reg}} \\ \text{Divergente} & \text{caso contrário} \end{cases}$$

Root recalculado:

$$H_{\text{root}}^{\text{rec}} = \text{SHA256}_{\text{hex}}( h_1^{\text{sub}} \Vert h_2^{\text{sub}} \Vert \cdots )$$

| Status global | Condição |
|---------------|----------|
| Íntegro | Todas as seções correspondem **e** hash do PDF bate com a emissão |
| Adulterado parcialmente | Pelo menos uma seção divergente **e** pelo menos uma correspondente |
| Totalmente inválido | Todas divergentes, ou seções batem mas hash binário não |
| Documento não reconhecido | Falha na identificação ou lacre ausente |

### PDF rasterizado (detalhe)

Sem texto vetorial extraível, $h_i^{\text{sub}}$ tende a $\varepsilon$ para todas as seções → **Totalmente inválido**. Visualmente idêntico, mas sem lacre semântico verificável. Esteganografia e XMP também costumam se perder no reprocessamento.

## Modelo de dados

**Lacre documental** — contrato, template, root hash, JSON de sub-hashes por seção, data de registro.

**Registro de emissão** — id da emissão, contrato, papel, hash binário pós-XMP, data, titular mascarado.

## Resposta da API

| Campo | Descrição |
|-------|-----------|
| `status` / `statusLabel` | Enum + rótulo em português |
| `isAuthentic` | `true` somente se íntegro (via XMP, sem fallback degradado) |
| `hashDiagnostic` | Hashes submetido vs. registrado |
| `sections[]` | Auditoria por seção |
| `originTrace` | Via de origem (emissão / titular mascarado) |
| `custodyNarrative` | Diagnóstico textual de custódia (cenário 3) |
| `validityGuidance` | Orientação prudente / disclaimer |
| `provenance` | Resolução (XMP, stego, nº contrato) e integridade binária |

## Demos na documentação

| Componente | Cenário |
|------------|---------|
| `<ValidationIntegroDemo />` | 1 — Íntegro |
| `<ValidationUnrecognizedDemo />` | 2 — Não reconhecido |
| `<ValidationAdulteradoDemo />` | 3 — Adulterado parcialmente |
| `<ValidationDecisionFlow />` | Árvore de decisão do validador |

Os previews usam dados ilustrativos — sem hashes, tokens ou identificadores reais.

## Conferência manual vs. automatizada

| Método | O que verifica |
|--------|----------------|
| Manual (usuário) | $H_{\text{pdf}}$ do arquivo vs. valor informado pelo sistema |
| `POST /api/validar` | Identidade + seções + root + emissão + adulteração parcial |

## Próximo

- [Hasher e lacre](/referencia/engenharia/hasher) — como $h_i$ e $H_{\text{root}}$ são calculados
- [Esteganografia](/referencia/engenharia/esteganografia) — rastreio de emissão
- [Visão geral](/referencia/engenharia/) — arquitetura completa
