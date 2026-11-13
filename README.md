# Context Engine — Motor de Contexto Governado

> Motor de contexto agêntico para o mercado imobiliário carioca:
> dado público, rastreabilidade de fonte e governança por entidade.

## 1. Nome

**Context Engine** — motor de contexto governado.

O nome diz o que o sistema faz: ele não gera resposta do zero, ele **monta o contexto** que torna uma resposta possível e verificável. "Governado" porque cada fato carrega origem, data e permissão.

## 2. Objetivo

Construir, em 90 dias, um motor de contexto que responde perguntas sobre o mercado imobiliário do município do Rio de Janeiro usando **exclusivamente fontes públicas**, com **citação de fonte em cada afirmação** e **controle de acesso por entidade**.

O motor não é um chatbot. É uma camada de contexto: recebe uma pergunta, resolve quais entidades do domínio são relevantes, recupera as evidências nas fontes e devolve a resposta com a origem de cada dado.

**Objetivo de aprendizado:** cobrir os seis anéis da engenharia agêntica (fundação, construção, harness, qualidade, escala e generalização) em um único repositório que evolui.

## 3. Intenção

Provar, em público e com número, que engenharia agêntica não é prompt bonito: é especificação, eval e governança. Cada entrega quinzenal traz um artefato clicável e uma métrica medida, não uma promessa.

O projeto é também uma transição deliberada: de engenheiro de dados que consome plataforma para engenheiro que constrói a camada agêntica sobre ela.

## 4. Contexto

### 4.1 O problema

Dado público imobiliário existe em quantidade. O que não existe é confiança. Um corretor, uma construtora ou um analista que precisa saber "qual o preço do m² neste bairro e de onde veio esse número" hoje encontra três respostas diferentes em três portais, sem conseguir dizer qual é a fonte, qual é a data de referência, ou se aquele número é preço pedido ou preço de transação.

O problema não é acesso ao dado. É **proveniência**: saber de onde veio, de quando é, e se aquele dado sustenta a afirmação que está sendo feita.

### 4.2 O domínio

Mercado imobiliário do município do Rio de Janeiro, com **ênfase na Zona Portuária** (Operação Urbana Porto Maravilha). O município inteiro permanece no escopo para servir de base de comparação.

### 4.3 As fontes

Somente dado público e aberto:

| Fonte | O que fornece | Granularidade | Atualização |
|---|---|---|---|
| ITBI Rio (DATA.RIO) | Transações reais de compra e venda | Logradouro / mês | Mensal |
| ITBI Rio (Fazenda) | Série histórica em planilha | Logradouro / mês | Mensal |
| FipeZap | Preço médio do m² | Município / mês | Mensal |
| IBGE | População, domicílios, renda, setores | Município / setor | Anual |
| ITBI Niterói (opcional) | Transações agregadas | Logradouro / ano | Anual |

Mapa completo em [`docs/fontes.md`](docs/fontes.md).

**Regra de comparabilidade:** o motor nunca compara fatos de granularidades diferentes. Fato mensal só se compara com mensal; anual só com anual.

### 4.4 A ontologia

Cinco entidades compartilhadas, as mesmas no domínio imobiliário e no domínio de crédito:

**empreendimento** · **unidade** · **cliente** · **proposta** · **contrato**

No MVP, apenas `empreendimento` e `unidade` são populadas com dado real. As outras três são modeladas e populadas com dado sintético, porque envolvem dado pessoal, que este projeto não ingere.

## 5. Metodologia — Spec-Driven Development

Este projeto é construído em **SDD**: a especificação vem antes do código, e nenhuma feature começa sem spec aprovado.

### 5.1 Hierarquia de documentos
-