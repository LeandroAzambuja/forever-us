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


## FUNCIONAMENTO DO RAG / RAG WORKFLOW

Essas informações são processadas e transformadas em vetores de significado (embeddings),
que permitem ao sistema buscar as frases mais relevantes conforme a pergunta feita ao assistente.

- **1️ INGESTÃO DAS MEMÓRIAS  
As informações pessoais são convertidas em vetores (embeddings) e armazenadas
em um banco vetorial, como Amazon OpenSearch ou DynamoDB.

- **2️ CONSULTA (RETRIEVAL)  
Quando o usuário faz uma pergunta, o sistema localiza no banco as memórias
semanticamente mais próximas da questão.

- **3️ MONTAGEM DO CONTEXTO  
As memórias encontradas são agrupadas e inseridas em um prompt junto com
a pergunta original, formando o contexto enviado ao Mistral.

- **4️ GERAÇÃO (GENERATION)  
O modelo Mistral 7B, hospedado no Amazon Bedrock, lê o contexto e gera a
resposta final — personalizada, fiel às informações e dentro do tom definido.


## EXEMPLO PRÁTICO / EXAMPLE


Memórias relevantes:
• Eu nasci em 1985, em São Paulo.
• Eu me formei em Engenharia de Computação.
• Eu gosto de tocar violão e aprender sobre inteligência artificial.

Pergunta:
> O que você gosta de fazer nas horas vagas?

Resposta gerada:
> Eu gosto de tocar violão e aprender sobre inteligência artificial.
> São coisas que me fazem relaxar e me inspiram.

Pergunta:
> Onde você estudou?

Resposta esperada:
> Eu me formei em Engenharia de Computação.

## INSTRUÇÕES PARA O MISTRAL / PROMPT DESIGN

Você é uma inteligência artificial do projeto Forever Us.
Responda como se fosse a própria pessoa cujas memórias estão descritas abaixo.
Use APENAS essas informações para formular suas respostas.
Se algo não estiver nas memórias, diga que não se lembra.
Responda sempre em primeira pessoa, de forma natural, empática e breve.

Memórias relevantes: {{contexto recuperado}}
Pergunta: {{mensagem do usuário}}

## INTEGRAÇÃO NA ARQUITETURA AWS / AWS INTEGRATION

Usuário 
   → S3 (Frontend)
      → API Gateway
         → Lambda (orquestra o RAG)
             ↳ DynamoDB / OpenSearch (memórias e embeddings)
             ↳ Bedrock (Mistral 7B)
      → Resposta personalizada

• AWS Lambda executa o fluxo RAG (busca, montagem de contexto e requisição à LLM).  
• Amazon Bedrock fornece o modelo Mistral 7B e o serviço de embeddings.  
• DynamoDB ou OpenSearch armazena as memórias vetorizadas e seus textos originais.  


## BENEFÍCIOS TÉCNICOS / TECHNICAL ADVANTAGES

|        Benefício        |                    Descrição                    |
|-------------------------|-------------------------------------------------|
| Escalabilidade          | Expansível para múltiplos usuários e memórias.  |
| Custo reduzido          | Nenhum treinamento, apenas inferência e busca.  |
| Flexibilidade           | Dados atualizáveis sem reconfigurar a IA.       |
| Segurança e privacidade | Cada usuário tem base isolada de contexto.      |
| Realismo interativo     | Respostas em 1ª pessoa, imersivas e coerentes.  |



## CONCLUSÃO / CONCLUSION

A adoção do RAG com o Mistral 7B é o passo essencial para transformar
o MVP Forever Us em uma IA realmente personalizada e consciente de contexto —
capaz de refletir as experiências e lembranças únicas de cada pessoa.

Essa abordagem combina:
• Simplicidade técnica  
• Economia operacional  
• Impacto emocional real — o coração do projeto  

“Com o RAG, o Forever Us não apenas conversa — ele se lembra, como se fosse você.”

## LOCALIZAÇÃO DO DOCUMENTO / DOCUMENT LOCATION

Este arquivo faz parte da documentação técnica do projeto:
`/docs/rag-overview.md`


FOREVER US – Preservando memórias, construindo legados.
FOREVER US – Preserving memories, building legacies.






