---
title: Parâmetros — precificação trânsito
description: Tabelas de percentual, multiplicadores de instância e valores base do art. 258 CTB
---

# Parâmetros — precificação trânsito

Página para o **time Anexus**. O modelo de cálculo explicado ao usuário final está em [Precificação de defesas de trânsito](/precificacao/transito).

## Fórmula

```
honorarios = percentual_servico × valor_base_gravidade × multiplicador_instancia
```

`valor_base_gravidade` vem da natureza da infração no art. 258 do CTB. O agravamento da multa no auto (`multiplicador_infracao` do CTB) **não entra** no honorário.

## Valores base — art. 258 CTB

Redação dada pela [Lei nº 13.281/16](https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2016/lei/l13281.htm). Texto consolidado: [CTB Digital — art. 258](https://ctbdigital.com.br/artigo/art258/). CTB: [Lei nº 9.503/97](https://www.planalto.gov.br/ccivil_03/leis/l9503compilado.htm).

| Natureza | `valor_base_gravidade` |
|----------|------------------------|
| Gravíssima | R$ 293,47 |
| Grave | R$ 195,23 |
| Média | R$ 130,16 |
| Leve | R$ 88,38 |

## Parâmetros comerciais Anexus

| Parâmetro | Valor | Notas |
|-----------|-------|-------|
| `percentual_servico` | **0,5** (50%) | Política comercial da Anexus sobre o valor base da gravidade; a instância ajusta pela complexidade |
| `multiplicador_instancia.defesa_previa` | **0,5** | |
| `multiplicador_instancia.indicacao_real_condutor` | **0,2** | |
| `multiplicador_instancia.jari` | **1** | |
| `multiplicador_instancia.cetran` | **1,2** | |

O percentual base de **50%** é a política comercial da Anexus sobre o valor base da gravidade; o multiplicador de instância ajusta esse valor conforme a complexidade do serviço. O Guia de trânsito usa estes valores nos exemplos.

## Vigência

- Contratos **já lacrados** antes de nova legislação ou de novos parâmetros comerciais **mantêm** o honorário acordado.
- Contratos **ainda não selados** usam a regra vigente no momento do fechamento / selo.

Rota de produto prevista (sem login): FAQ em `/faq`. Ver [Status de implementação](/referencia/status-implementacao).

## Ver também

- [Precificação (Guia)](/precificacao/)
- [O que o honorário cobre](/precificacao/escopo)
- [Precificação de defesas de trânsito](/precificacao/transito)
- [Pedido e valores](/dominios/contratos-pedido)
