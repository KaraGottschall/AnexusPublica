---
title: Engenharia — integridade documental
description: Arquitetura técnica do lacre, pipeline LaTeX, hasher por seções, esteganografia e validação forense
---

# Engenharia — integridade documental

Documentação técnica para o time Anexus. Descreve como a plataforma **gera**, **lacra** e **valida** PDFs oficiais — complementando a explicação de produto em [Assinatura e integridade](/contratos/assinatura).

O sistema opera em três fases:

1. **Registro** — compila o PDF canônico, extrai texto por seção, calcula hashes e persiste o lacre.
2. **Emissão** — gera cópias personalizadas com esteganografia zero-width, metadados XMP e hash binário.
3. **Validação** — recebe um PDF externo, relê XMP e seções, e compara com o registro.

## Arquitetura

No **registro**, o contrato passa por montagem LaTeX, compilação pdfLaTeX, extração de texto e cálculo de hashes por seção, resultando no lacre documental persistido.

Na **emissão**, o lacre alimenta a geração de cópias personalizadas: o codec esteganográfico marca cada cópia, o PDF é recompilado e recebe metadados XMP, e o registro de emissão guarda o hash binário.

Na **validação**, o endpoint público recebe um PDF e o validador forense reutiliza extração, hashing, esteganografia e XMP para comparar o arquivo submetido com o lacre e com os registros de emissão.

## Componentes

| Componente | Responsabilidade |
|------------|------------------|
| Serviço de integridade | Orquestra registro e emissão |
| Montador LaTeX | Monta os dados do documento e escolhe o template |
| Compilador pdfLaTeX | Executa duas passagens de compilação em diretório temporário |
| Extrator de texto PDF | Extrai texto completo e por seção do PDF |
| Normalizador canônico | Normalização determinística antes do hash |
| Computador de hash por seção | SHA-256 em representação hexadecimal minúscula |
| Codec esteganográfico | Codifica e decodifica identificador de emissão em zero-width |
| Serviço XMP | Injeta e lê metadados Anexus no PDF |
| Validador forense | Valida PDF submetido contra o registro |

Templates LaTeX ficam em assets dedicados do backend; a lógica de documentos reside na camada de infraestrutura.

## Nesta seção

| Página | Conteúdo |
|--------|----------|
| [Pipeline LaTeX](/referencia/engenharia/pipeline-latex) | Templates, montagem de dados e compilação pdfLaTeX |
| [Hasher e lacre](/referencia/engenharia/hasher) | Normalização, hash por seção, root hash |
| [Esteganografia](/referencia/engenharia/esteganografia) | Payload zero-width, codificação/decodificação, interação com o hasher |
| [Validação forense](/referencia/engenharia/validacao-forense) | Endpoint público, três cenários de parecer (íntegro / não reconhecido / adulterado parcialmente), XMP e status por seção |

## Relação com produto

| Conceito de produto | Implementação |
|---------------------|---------------|
| Lacre do PDF | Root hash + hashes por seção |
| Documento oficial | Emissão com XMP + hash binário do PDF |
| Conferir integridade | Manual (SHA-256 do arquivo) ou validação via API |
| Prévia inválida | PDF sem registro de emissão oficial — ver [Assinatura](/contratos/assinatura#previa-invalida-e-documento-oficial) |
