---
title: Atores
description: Papéis no contrato — Contratante, Anexus e Beneficiário
---

# Atores

Na Anexus, **atores** são os papéis que participam de um contrato de **serviço documental**. Não são três cadastros iguais: cada um tem responsabilidades, assinatura e acesso distintos.

O [tipo de serviço](/tipos-de-servico/) (trânsito, outro ou demais áreas) não muda quem são os atores — muda o que entra no pedido e nas etapas.

## Os três papéis

| Ator | Papel resumido | Assina no portal? | Paga? | Portal? |
|------|----------------|:-----------------:|:-----:|:-------:|
| [Contratante](atores-contratante) | Quem contrata e em cujo nome o operador aceita e paga | Não | Honorários, via operador | Não |
| [Anexus](atores-anexus) | Plataforma (operadora); o **operador** age na área interna | Não | Não | Não (área interna) |
| [Beneficiário](atores-beneficiario) | Titular pontual do serviço (a quem o documento ou o caso se refere) | Não | Não | Sim (stepper e dossiê) |

O **operador** é o usuário autenticado na área interna — sempre **controlador** dos dados. A Anexus é a plataforma em que ele age, não uma pessoa que assina ou opera.

O PDF do contrato é **pré-assinado pelo operador** na conferência do pedido. Fluxo completo: [Assinatura e integridade](contratos-assinatura).

## Como se relacionam

<ActorsFlow />

O **contrato** é o eixo: liga contratante, plataforma e, quando houver, beneficiário. O operador cria, confere e paga o contrato pela área interna; o beneficiário acompanha o processo no [Portal](/telas/portal/) sem assinar.

O beneficiário **não** é um cadastro próprio no sistema — nome, documento e e-mail ficam no serviço vinculado ao contrato. Já o contratante é o cliente recorrente.

## Papel contratual e papel na LGPD

Os atores acima descrevem o **contrato**. O tratamento de dados pessoais tem papéis próprios:

| Quem | Papel contratual | Papel na LGPD |
|------|------------------|---------------|
| Usuário autenticado (operador) | Age na área interna: cria contratos, confirma termos, paga, atualiza etapas | **Controlador** |
| [Anexus](atores-anexus) | Plataforma: pedido, dossiê, portal e lacre | **Operadora** |
| [Contratante](atores-contratante) | Assina e paga | Parte contratual; titular dos próprios dados |
| [Beneficiário](atores-beneficiario) | Acompanha o serviço | **Titular** dos dados do caso |

O controlador **é** o cadastro autenticado na área interna — não um quarto papel. Detalhes: [Papéis no tratamento](/privacidade/papeis).

## Conta e organização

Os atores acima são papéis **no contrato**. A **conta de usuário** e a **organização** (espaço de trabalho na área interna) são outra camada — ver [Organização](organizacao). Quem está logado na área interna é o controlador daquele tratamento.

## Documentos e acesso

Para saber **como e quando** cada parte vê o contrato, o dossiê e as etapas, leia [Documentos e acesso](/telas/portal/documentos) e [Progresso e notificações](contratos-progresso).