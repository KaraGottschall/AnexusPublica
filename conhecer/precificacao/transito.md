---
title: Precificação de defesas de trânsito
description: Como os honorários de defesa de trânsito são calculados a partir da gravidade e da instância
---

# Precificação de defesas de trânsito

Este é o preço do [tipo de serviço Trânsito](/tipos-de-servico/transito). O honorário é calculado em função do **valor base da gravidade** (art. 258 do CTB) e da **instância** do serviço (por exemplo, defesa prévia no DETRAN, JARI ou CETRAN).

Honorários **não são a multa**: a multa é a referência legal; o honorário é o preço do trabalho contratado. O agravamento da multa no CTB (fator multiplicador do governo) **não entra** no honorário. O que está incluso no serviço: [O que o honorário cobre](/precificacao/escopo).

## Fontes legais

Os valores base por gravidade da infração vêm do **art. 258** do Código de Trânsito Brasileiro (CTB):

- [Lei nº 9.503/97 (CTB consolidado)](https://www.planalto.gov.br/ccivil_03/leis/l9503compilado.htm)
- [Lei nº 13.281/16](https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2016/lei/l13281.htm) — redação do art. 258
- [Art. 258 — CTB Digital](https://ctbdigital.com.br/artigo/art258/) — texto e valores consolidados

Esses valores **podem ser atualizados** por legislação ou atos do CONTRAN. A documentação usa a redação citada acima; em caso de divergência, prevalece a norma vigente. Ver também [Vigência de legislação e parâmetros](#vigencia-de-legislacao-e-parametros).

## Valores base por gravidade

As infrações punidas com multa classificam-se em quatro categorias (art. 258):

| Natureza | Valor base |
|----------|------------|
| **Gravíssima** | R$ 293,47 |
| **Grave** | R$ 195,23 |
| **Média** | R$ 130,16 |
| **Leve** | R$ 88,38 |

A **gravidade** vem do enquadramento da infração no auto (AIT) e na legislação — não de uma descrição genérica do pedido.

## Instâncias do serviço

A **instância** indica em qual etapa do processo administrativo a defesa será apresentada. Ela afeta a complexidade do serviço e, por isso, entra no cálculo com um **multiplicador de instância**:

| Instância | Contexto típico | Multiplicador |
|-----------|-----------------|---------------|
| **Defesa prévia** | Impugnação perante o órgão autuador (ex.: DETRAN, PRF, município) | 0,5 |
| **Indicação de real condutor** | Identificação de quem conduzia o veículo | 0,2 |
| **JARI** | Recurso à Junta Administrativa de Recursos de Infrações | 1 |
| **CETRAN** | Recurso ao Conselho Estadual de Trânsito | 1,2 |

O **percentual base de 50%** (0,5) é a política comercial da Anexus sobre o valor base da gravidade; a **instância** ajusta esse valor conforme a complexidade do serviço. Detalhe técnico dos parâmetros: [Referência — parâmetros de precificação](/referencia/parametros-precificacao-transito).

## Como o honorário é calculado

```
honorários = percentual do serviço × valor base da gravidade × multiplicador da instância
```

Com os parâmetros atuais, o percentual do serviço é **0,5** (50%). O multiplicador da multa no CTB (agravamento) não entra nesta conta.

<PricingFlow />

### Exemplos

**Exemplo 1 — defesa prévia, infração grave**

- Valor base: R$ 195,23  
- honorários = 0,5 × 195,23 × 0,5 = **R$ 48,81**

**Exemplo 2 — mesma infração, instância JARI**

- honorários = 0,5 × 195,23 × 1 = **R$ 97,62**

**Exemplo 3 — indicação de real condutor, infração leve**

- Valor base: R$ 88,38  
- honorários = 0,5 × 88,38 × 0,2 = **R$ 8,84**

**Exemplo 4 — CETRAN, infração gravíssima** (ex.: recusa aos procedimentos do art. 277)

- Valor base: R$ 293,47  
- honorários = 0,5 × 293,47 × 1,2 = **R$ 176,08**

A multa no auto pode ser agravada pelo governo (por exemplo, ×10). Isso não altera o honorário Anexus: continua o valor da tabela abaixo.

Só a troca da instância (defesa prévia → JARI) altera o honorário, mantendo a mesma gravidade.

## Tabela rápida

Valores com percentual **0,5** e multiplicadores de instância vigentes.

| Gravidade | Defesa prévia | Indicação | JARI | CETRAN |
|-----------|---------------|-----------|------|--------|
| Gravíssima | R$ 73,37 | R$ 29,35 | R$ 146,74 | R$ 176,08 |
| Grave | R$ 48,81 | R$ 19,52 | R$ 97,62 | R$ 117,14 |
| Média | R$ 32,54 | R$ 13,02 | R$ 65,08 | R$ 78,10 |
| Leve | R$ 22,10 | R$ 8,84 | R$ 44,19 | R$ 53,03 |

## Vigência de legislação e parâmetros

- Contratos **já lacrados** antes do início de vigência de nova legislação (ou de novos parâmetros comerciais) **permanecem** com o honorário acordado.
- Contratos **ainda não selados** usam a regra vigente no momento do **fechamento** / selo.

## Na prática no contrato

Para **trânsito**, o **AIT (auto de infração)** é **indispensável** para fechar o preço e avançar para documento e aceite: sem ele o operador não confirma a gravidade nem o honorário. O pedido pode ser iniciado de forma parcial; o fechamento exige o AIT.

Com tipo de defesa, instância e AIT, o sistema apresenta o **honorário fechado** daquele serviço.

Detalhes dos campos do pedido: [Pedido e valores](/dominios/contratos-pedido). Visão do tipo: [Trânsito](/tipos-de-servico/transito).

[← Voltar a Precificação](/precificacao/)
