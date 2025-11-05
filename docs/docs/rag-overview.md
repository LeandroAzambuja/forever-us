# Forever Us – Integração RAG com Mistral 7B

**Data:** 05/11/2025  
**Autor:** Leandro C. Azambuja  
**Projeto:** Forever Us – Sistema de Legado Digital e Simulação de Personalidade 

## Sobre o Conceito / About the Concept

O **RAG (Retrieval-Augmented Generation)** é uma abordagem moderna que permite combinar o poder de um modelo de linguagem com dados personalizados externos — chamados de **memórias** — sem precisar realizar treinamento direto no modelo.

Em vez de “ensinar” o Mistral 7B por meio de fine-tuning, o RAG **fornece ao modelo o contexto necessário no momento da geração da resposta**.  
Isso permite criar interações altamente personalizadas, reduzindo custos e aumentando a flexibilidade.

> Em resumo: o modelo não aprende de forma permanente, mas responde como se “lembrasse” de informações específicas.

---

## Por que utilizar o RAG no Forever Us / Why Use RAG

O objetivo do **Forever Us** é criar uma inteligência artificial capaz de representar e preservar memórias pessoais de indivíduos.  
Cada pessoa deve ter uma “presença digital” única, baseada em suas próprias informações e experiências.  

Com o RAG, conseguimos:

- **Reduzir custos** — não há necessidade de treinar ou ajustar modelos.  
- **Manter flexibilidade** — as memórias podem ser atualizadas ou removidas a qualquer momento.  
- **Separar contextos** — cada usuário pode ter seu próprio banco de memórias.  
- **Gerar respostas mais humanas e contextualizadas** — baseadas em dados reais do indivíduo.  

> O RAG é o elo entre o modelo genérico (Mistral 7B) e as informações pessoais armazenadas no projeto.

---

## Estrutura de Memórias / Memory Structure

Cada usuário do MVP terá um conjunto de **200 a 300 informações pessoais** extraídas de um questionário, formando sua base de memórias.  
Esses dados serão armazenados de forma estruturada, em formato JSON, por exemplo:

```json
[
  { "id": 1, "text": "Eu nasci em Porto Alegre, no sul do Brasil." },
  { "id": 2, "text": "Eu sou formado em Engenharia de Computação." },
  { "id": 3, "text": "Eu gosto de trabalhar com segurança da informação e computação em nuvem." }
]
