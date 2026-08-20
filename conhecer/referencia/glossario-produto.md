---
title: Glossário de produto
description: Vocabulário preferido, papéis LGPD e o que não entra no Guia
---

# Glossário de produto

Página para o **time Anexus**. Evita regressão de linguagem depois do realinhamento de visão (agosto de 2026). O [Guia](/) usa estes termos no texto conceitual; rótulos de tela continuam fiéis ao aplicativo.

## Posicionamento

A Anexus é uma **plataforma de serviços documentais**: pedido, dossiê e transparência de etapas. Não é “SaaS de defesas de trânsito”. Trânsito é o **primeiro tipo de serviço documentado**, não o produto inteiro.

A Anexus é **entidade não física**: opera os dados como **operadora** LGPD. Quem usa a conta autenticada é sempre **controladora**.

Pilares (Guia): [Plataforma](/plataforma).

## Vocabulário

| Termo preferido (Guia) | Evitar como default | Rótulo na UI hoje |
|------------------------|---------------------|-------------------|
| tipo de serviço | tipo de defesa (em texto conceitual) | Tipo de serviço |
| documento / peça | defesa (quando genérico) | — |
| etapa do serviço | fase da defesa | badges na lista (rótulo do tipo) |
| usuário controlador | profissional controlador | — |
| operador | equipe Anexus / a Anexus (como pessoa) | — |
| **organização** | tenant, workspace, empresa (genérico) | — |
| **conta de usuário** | login, cadastro (sem distinguir org) | — |
| **perfil na organização** | cargo, função LGPD | — |
| serviço contratado / serviço documental | serviço de defesa | — |
| honorários do serviço | honorários da defesa (quando genérico) | Honorários |
| **prévia inválida** | PDF “oficial” baixado antes da baixa; rascunho sem marca d'água | — |
| **documento oficial** | qualquer PDF do contrato; prévia com hash | — |

“Defesa” permanece correto em **trânsito** (tipo de serviço, instância, peça, indeferimento). O cadastro usa o rótulo **Tipo de serviço** (Trânsito, Outro, Locação).

**Locação** está no catálogo da tela, mas o pedido ainda não é concluível — [Status de implementação](/referencia/status-implementacao).

**Prévia inválida:** exportação do contrato **antes da baixa**; marca d'água; valores fictícios ou embaralhados; sem valor de instrumento oficial. **Documento oficial:** PDF lacrado após o pagamento no portal; download e envio externo **após a baixa** (encerramento do serviço). Detalhe no Guia: [Prévia inválida e documento oficial](/dominios/contratos-assinatura#previa-invalida-e-documento-oficial).

Advogado, despachante ou equivalente são **exemplos** de quem usa a conta — não um quarto papel LGPD.

Detalhe no Guia: [Organização](/dominios/organizacao).

## Papéis LGPD

| Papel | Quem |
|-------|------|
| **Controlador** | Usuário autenticado na área interna — sempre, na própria organização ou na de outro. Decide as finalidades do tratamento |
| **Operadora** | Anexus — a plataforma (entidade não física). Trata dados conforme as instruções do controlador. Nunca é controladora |
| **Contratante** | Parte que assina e paga; pode coincidir com o usuário ou com o titular |
| **Titular** | Beneficiário do serviço (quando identificado); o contratante também pode ser titular dos próprios dados |

Detalhe no Guia: [Papéis no tratamento](/privacidade/papeis).

## Ciclo de vida e estatísticas

| Termo | Significado no Guia |
|-------|---------------------|
| **Anonimização** | Após a baixa e a entrega, a plataforma remove identificadores e destrói a ligação pessoa ↔ caso |
| **Relatório de tratamento** | Linha do tempo do que aconteceu com os dados do caso (anexos, etapas, acessos) |
| **Dados agregados** | Estatísticas sem identificação individual (ex.: faixa etária + tipo de serviço), retidas após a anonimização |

Detalhe no Guia: [Como meus dados são usados](/privacidade/uso-dos-dados) e [Ciclo de vida dos dados](/privacidade/ciclo-de-vida-dos-dados).

## O que não documentar no Guia

- Renomeação residual no código (`tipoDefesa` em partes do domínio; a UI já diz **Tipo de serviço**)
- Promessas de features não existentes no produto (exceto menção **em progresso para implementação** em itens críticos, como assinatura ICP-Brasil e Locação)
- Termos de implementação (SPA, mock, fixture, localhost) no prose do Guia
- Anexus como pessoa, equipe ou signatária

## Ver também

- [Plataforma](/plataforma)
- [Organização](/dominios/organizacao)
- [Tipos de serviço](/tipos-de-servico/)
- [Privacidade de Dados](/privacidade/)
- [Status de implementação](/referencia/status-implementacao)
- [Publicar atualizações](/referencia/publicar-atualizacoes)
- [Contribuir](/referencia/contribuir)
