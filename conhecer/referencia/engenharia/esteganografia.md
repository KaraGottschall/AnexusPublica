---
title: Esteganografia zero-width
description: Codificação de identificador de emissão e papel do signatário em caracteres Unicode invisíveis no PDF
---

# Esteganografia zero-width

Cada **cópia emitida** do documento carrega um identificador invisível embutido no texto do PDF. O sistema codifica o identificador da emissão e o papel do signatário usando caracteres Unicode de largura zero — imperceptíveis visualmente, mas extraíveis pelo validador forense.

## Quando é aplicada

Na emissão de cópia, o fluxo é: geração do ID de emissão → codificação zero-width → injeção do prefixo nos dados LaTeX → compilação → PDF emitido. Na validação, o texto é extraído e o payload decodificado.

| Fase | Prefixo esteganográfico | Motivo |
|------|-------------------------|--------|
| Registro | ausente | PDF canônico — sem marca de emissão |
| Emissão | string codificada | Rastreia qual cópia foi entregue a quem |

## Payload

A string codificada é:

$$p = \texttt{id} \Vert \texttt{"|"} \Vert \texttt{roleInt}$$

onde `id` é o identificador da emissão (GUID compacto) e `roleInt` é o valor inteiro do papel do signatário (ex.: Contratante = 0, Titular = 1, …).

## Codificação binária

Cada byte $b_j$ de $p$ (UTF-8) vira 8 bits MSB-first. Cada bit mapeia para um caractere zero-width:

| Bit | Caractere | Code point |
|-----|-----------|------------|
| 0 | zero-width space | U+200B |
| 1 | zero-width non-joiner | U+200C |

A string final é delimitada:

$$\sigma(p) = \texttt{FEFF} \Vert b_1 b_2 \cdots b_{8|p|} \Vert \texttt{U+200D}$$

| Delimitador | Code point | Função |
|-------------|------------|--------|
| Início | U+FEFF (BOM) | Marca o início do payload |
| Bits | U+200B / U+200C | Dados |
| Fim | U+200D (ZWJ) | Marca o fim do payload |

O processo de codificação:

1. Monta a string `id|roleInt` em UTF-8.
2. Converte cada byte em 8 bits, MSB primeiro.
3. Mapeia cada bit para U+200B (0) ou U+200C (1).
4. Envolve a sequência com delimitadores de início (U+FEFF) e fim (U+200D).

## Onde aparece no documento

$\sigma(p)$ é inserido no início dos dados LaTeX antes da compilação. Após compilação, o texto fica embutido no fluxo tipográfico do PDF — invisível na renderização, mas presente na extração de texto.

## Decodificação

Na validação forense, o sistema tenta decodificar o payload a partir do texto extraído:

1. Localiza o delimitador de início (U+FEFF) e o de fim (U+200D).
2. Lê a sequência de bits entre os delimitadores.
3. Agrupa em bytes (8 bits cada).
4. Decodifica UTF-8 → string `id|roleInt`.
5. Retorna o par emissão/papel ou indica ausência de payload válido.

Se os delimitadores não forem encontrados ou a decodificação falhar, o payload é considerado inválido.

## Interação com o hasher

A normalização canônica **remove** caracteres zero-width antes de calcular $h_i$:

$$N(t) = \text{trim}\big(\text{ws}( \text{NFC}(\text{stripZW}(t)) ) \big)$$

Logo:

- $h_i$ e $H_{\text{root}}$ **não dependem** do payload esteganográfico.
- Emissões distintas (IDs diferentes) compartilham o **mesmo lacre de conteúdo** se o texto visível for idêntico.
- A esteganografia identifica **qual emissão** entregou aquela cópia, não altera o lacre semântico.

Isso é intencional: adulteração de conteúdo é detectada pelo hasher; rastreio de proveniência é feito pela esteganografia, XMP e registro de emissão.

## Metadados complementares

Além da esteganografia, cada emissão recebe:

- **XMP** no PDF (contractId, emissionId, templateId, rootHash)
- **Registro de emissão** (hash do PDF, papel, data de emissão, nome e documento mascarados)

A validação tenta identificar a emissão pela esteganografia; se falhar, faz fallback por hash binário do PDF.

## Próximo

- [Validação forense](/referencia/engenharia/validacao-forense) — como stego, XMP e hasher se combinam na conferência
- [Hasher e lacre](/referencia/engenharia/hasher) — normalização e remoção de zero-width
