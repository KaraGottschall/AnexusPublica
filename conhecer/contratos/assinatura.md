---
title: Assinatura e integridade
description: Como o contrato é assinado, lacrado e conferido com hash SHA-256
---

# Assinatura e integridade

Esta página explica **como o contrato é assinado** na Anexus, **quais dados** entram na assinatura, o que é o **hash SHA-256**, a diferença entre **prévia inválida** e **documento oficial**, e como **conferir** se a cópia do PDF ainda é a mesma que o sistema lacrou.

## O que é a assinatura na Anexus

**Assinatura com certificado ICP-Brasil:** em progresso para implementação. Hoje, o contrato usa **aceite eletrônico interno**: o operador confirma os termos **em nome do [contratante](/atores/contratante)** na área interna, e o sistema registra esse ato (identidade do operador, data e hora).

O [beneficiário](/atores/beneficiario) **não assina** o contrato — acompanha as etapas e o dossiê no [Portal](/telas/portal/) depois da ativação, quando há e-mail e link.

## As três etapas

Do rascunho ao lacre, o instrumento passa por três momentos principais (as fases completas do contrato estão em [Documentos e acesso](/telas/portal/documentos)):

<ContractPhasesFlow />

1. **Pré-assinatura do operador** — na conferência do pedido, o PDF já sai com a assinatura do usuário autenticado, registrada pela plataforma. Qualquer exportação neste momento é **prévia inválida**.
2. **Aceite em nome do contratante** — o operador revisa as informações **na tela** (valores e cláusulas reais) e confirma os termos no quarto passo do cadastro ou na página do contrato.
3. **Lacre do PDF** — após a confirmação do **pagamento na área interna**, o sistema recompila o PDF, calcula o hash de integridade **SHA-256** e lacra o documento. O **envio e o download do PDF oficial** para as partes externas só ocorrem após a [baixa](/telas/contratos/lista) do serviço.

## Pagamento e baixa

| Momento | O que acontece |
|---------|----------------|
| **Pagamento na área interna** | Único pagamento dos honorários (após a conferência dos termos); confirma o lacre e ativa o contrato |
| **Baixa** | Encerramento operacional pelo operador; libera o PDF **oficial** no dossiê — **não** é cobrança |

## Dados usados em cada etapa

| Etapa | Quem | Dados registrados |
|-------|------|-------------------|
| **Pré-assinatura** | Operador (usuário autenticado) | Nome e documento de quem conferiu; conteúdo do contrato a partir do [pedido](/contratos/pedido) |
| **Aceite** | Operador em nome do [contratante](/atores/contratante) | Confirmação explícita na tela, data e hora |
| **Lacre** | Plataforma | PDF final com a legenda da assinatura do operador; **hash SHA-256** do arquivo |

Na linha de assinatura do PDF, o texto **abaixo** da linha de assinar segue este formato:

```
Anexus — [Nome completo do operador]
[Documento do operador]
```

`Anexus —` é o rótulo da plataforma; o nome e o documento são a identidade do controlador que disparou o envio. Detalhes da legenda na área interna: [Lista e operações](/telas/contratos/lista#assinatura-anexus-no-pdf).

## Como o operador confirma

1. Preenche o pedido na área interna e chega ao passo **Conferir informações**.
2. **Revisa na tela** o instrumento com valores e cláusulas **reais**.
3. Marca que leu e aceita os termos **em nome do contratante** e escolhe **Confirmar e pagar** (ou salva rascunho para pagar depois na página do contrato).

Após a confirmação do **pagamento na área interna**, o PDF é recompilado e lacrado, e o contrato fica ativo. Se houver e-mail do beneficiário, a plataforma envia o **link** do portal. O download do **documento oficial** só ocorre após a **baixa** do serviço.

## Prévia inválida e documento oficial {#previa-invalida-e-documento-oficial}

A **prévia inválida** é o arquivo que o beneficiário pode **baixar** no portal antes da baixa do serviço. Ela existe para consultar o formato do instrumento, **não** para assinar fora da plataforma nem para usar como contrato.

A prévia inválida traz **marca d'água**, rótulo de documento não válido e **valores fictícios ou embaralhados**. A pré-assinatura do operador pode aparecer visualmente; o arquivo **não** é o instrumento oficial e **não** confere com o hash do lacre.

O **documento oficial** é o PDF lacrado após o pagamento na área interna, com valores reais e hash SHA-256 registrado. Fica disponível para **download no dossiê** e para **envio por e-mail** só depois da **baixa** do serviço.

Isso impede que alguém baixe um PDF parecido com o real e o use como se fosse o instrumento da plataforma. O aceite válido e o documento oficial ficam vinculados ao registro interno (operador, lacre, hash).

O que **não muda**:

- O operador **vê valores e cláusulas reais na tela** antes de confirmar.
- O lacre e o SHA-256 acontecem após o pagamento na área interna — registro da plataforma.
- A conferência de integridade só se aplica ao **documento oficial** (após a baixa).
- O operador, na área interna, consulta o instrumento lacrado para operar o caso; a política de prévia inválida no download foca no [Portal](/telas/portal/).

| Momento | Na tela (portal) | Download ou e-mail |
|---------|------------------|--------------------|
| **Antes do pagamento** | Instrumento com valores e cláusulas reais (área interna) | Só **prévia inválida** |
| **Após pagamento e lacre, antes da baixa** | Stepper, dossiê e anexos no portal do beneficiário | Contrato: ainda **prévia inválida**; **sem** envio do PDF oficial |
| **Após a baixa** | Igual | **PDF oficial lacrado** — download no dossiê, hash válido, envio permitido |

Detalhes de acesso por fase: [Documentos e acesso](/telas/portal/documentos). Download no dossiê: [Dossiê](/telas/portal/dossie).

## O que é o hash SHA-256

O **hash** (aqui, **SHA-256**) é uma espécie de **impressão digital** do arquivo PDF lacrado: uma sequência fixa de caracteres calculada a partir do conteúdo do arquivo.

- Se o arquivo for **idêntico** ao lacrado, o hash calculado é sempre o mesmo.
- Se **qualquer bit** do arquivo mudar (edição, regravação, corrupção), o hash muda.

No momento do lacre, o sistema calcula o SHA-256 do PDF final e **guarda** esse valor. Assim dá para saber, depois, se uma cópia ainda corresponde ao **documento oficial**. A **prévia inválida** não bate com esse hash — isso é esperado.

## Conferir a integridade do contrato

A comparação de hash só se aplica ao **documento oficial**, disponível no [dossiê](/telas/portal/dossie) **após a baixa**. Quem tem acesso ao contrato baixado (contratante, beneficiário identificado ou operador) pode:

1. Baixar a **cópia oficial** do PDF do contrato no dossiê (depois da baixa).
2. Calcular o **SHA-256** desse arquivo com uma ferramenta confiável (utilitário do sistema operacional ou verificador de hash de confiança).
3. Comparar o resultado com o valor **informado pelo sistema** no lacre (por exemplo, no registro do contrato ou na comunicação após a baixa).

| Resultado | O que significa |
|-----------|-----------------|
| **Bate** | O arquivo é **idêntico** ao PDF lacrado — a integridade foi preservada. |
| **Não bate** | O arquivo foi **alterado**, corrompido, é uma **prévia inválida** ou **não é** a mesma versão — não trate essa cópia como o instrumento oficial. |

Use sempre a cópia oficial baixada do dossiê **após a baixa** (ou o PDF enviado pelo sistema nesse momento), não uma prévia inválida, uma versão antiga ou um arquivo editado à mão.

## Casos especiais

| Situação | Comportamento |
|----------|---------------|
| **Reenviar o portal** | Gera um novo link para o beneficiário e invalida o anterior; a **pré-assinatura do operador** já registrada **não** muda. |
| **Contrato lacrado** | Não pode mais ser editado; o PDF oficial é o lacrado com o hash registrado. Download e envio às partes externas só após a baixa. |

## Próximo

- [Progresso e notificações](/contratos/progresso) — stepper depois da ativação
- [Portal](/telas/portal/) — dossiê do beneficiário
- [Dossiê](/telas/portal/dossie) — prévia inválida até a baixa; PDF oficial depois
- [Lista e operações](/telas/contratos/lista) — conferência, pagamento e pré-assinatura na área interna

[← Voltar a Contratos](/contratos/)
