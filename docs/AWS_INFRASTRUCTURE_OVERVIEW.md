# 🧠 Forever Us – Arquitetura AWS (MVP da LLM)

## 🌎 Visão Geral / Overview

O **MVP do Forever Us** foi projetado para demonstrar a integração de uma **LLM (Large Language Model)** hospedada na **AWS**, com foco em **baixo custo**, **escalabilidade** e **simplicidade operacional**.  
A arquitetura garante que o **frontend**, o **backend** e o **modelo de linguagem** se comuniquem de forma eficiente, segura e sem desperdício de recursos.

---

## 🧩 Estrutura da Arquitetura / Architecture Structure

```
[Usuário] 
   ↓
[CloudFront]
   ↓
[S3 (Frontend)]
   ↓ (via API JavaScript)
[API Gateway]
   ↓
[AWS Lambda ↔ DynamoDB]
   ↓
[Bedrock (Mistral 7B)]
```

Essa topologia mostra o caminho completo de uma requisição — desde o acesso do usuário até o processamento pelo modelo de linguagem e o retorno da resposta.

---

## 🖥️ Frontend

**Serviços:** `Amazon S3` | `Amazon CloudFront`  

- **S3 (Simple Storage Service)** hospeda o site estático, contendo arquivos HTML, CSS e JavaScript.  
  É simples, seguro e de custo muito baixo.  
- **CloudFront** (opcional) distribui o conteúdo globalmente, reduzindo a latência e melhorando a performance.  

> O frontend é a camada sempre ativa, com custo praticamente nulo.

---

## ⚙️ Backend

**Serviços:** `Amazon API Gateway` | `AWS Lambda` | `Amazon DynamoDB`

- **API Gateway** atua como porta de entrada das requisições vindas do site, repassando-as com segurança para o backend.  
- **AWS Lambda** processa cada requisição sob demanda, conectando-se ao modelo e retornando a resposta ao usuário.  
  É **serverless** e **paga-se apenas pelo uso efetivo**.  
- **DynamoDB** registra logs e histórico de conversas, garantindo persistência leve entre execuções.

> Essa camada é responsável pela lógica do sistema e pela ponte entre o site e a LLM.

---

## 🧠 LLM – Cérebro da Aplicação

**Serviço:** `Amazon Bedrock` (Modelo **Mistral 7B**)

- A camada de IA utiliza o **Amazon Bedrock**, serviço gerenciado da AWS que oferece acesso direto a modelos de linguagem de última geração.  
- O modelo **Mistral 7B** foi escolhido pelo equilíbrio entre custo e desempenho.  
- Caso o Bedrock não esteja disponível, o modelo pode ser executado em uma **instância EC2** temporária, ativada apenas durante os testes.

> Essa camada é o coração do MVP, responsável por gerar respostas em linguagem natural.

---

## 🔍 Monitoramento e Custos

**Serviços:** `Amazon CloudWatch` | `AWS Budgets`

- **CloudWatch** coleta métricas, logs e monitora a saúde dos serviços.  
- **AWS Budgets** envia alertas quando o consumo se aproxima do limite de créditos definido.  

> O objetivo é garantir previsibilidade financeira e evitar custos desnecessários.

---

## 💰 Estratégia de Economia

1. **A IA (Bedrock/EC2)** só é ligada durante os testes.  
2. Após o uso, é desligada manualmente para evitar cobranças adicionais.  
3. **S3, Lambda e API Gateway** permanecem ativos, com custo quase nulo.  
4. **DynamoDB** usa o modo “sob demanda”, economizando leitura e escrita.

> Essa estratégia garante que o MVP possa ser testado continuamente sem exceder os créditos AWS Educate/Restart.

---

## 🔄 Fluxo de Comunicação / Data Flow

```
1. O usuário acessa o site hospedado no **S3** (opcionalmente acelerado via **CloudFront**).  
2. Ao enviar uma mensagem, o **JavaScript** do frontend chama o **API Gateway**.  
3. O **API Gateway** repassa o pedido para uma **função Lambda**.  
4. A **Lambda** envia a requisição à **LLM (Mistral 7B no Bedrock)** e armazena logs no **DynamoDB**.  
5. A resposta da LLM retorna pelo mesmo caminho até o navegador do usuário.
```

---

## 📊 Métricas Recomendadas

```
- Disponibilidade da instância de IA (Bedrock/EC2)  
- Tempo médio de resposta (latência total)  
- Volume de requisições processadas  
- Custo mensal total dos serviços  
- Logs de erro e uso de memória via CloudWatch  
```

---

## 🔮 Possíveis Extensões / Future Enhancements

```
- Suporte a modelos multimodais (texto, voz, imagem)  
- Processamento assíncrono com SQS ou Step Functions  
- Uso de containers gerenciados (ECS ou EKS)  
- Automação do ciclo de inicialização/desligamento da IA  
- Escalabilidade automática com base em demanda real  
```

---

## 🧾 Conclusão

A arquitetura AWS do **Forever Us – MVP da LLM** foi construída com base em três pilares:
**simplicidade, eficiência e economia**.  
Ela demonstra que é possível integrar um modelo de linguagem robusto em um ambiente cloud de baixo custo, mantendo segurança, modularidade e possibilidade de expansão futura.

> “Pequeno no custo, grande na ideia.” – Filosofia do MVP Forever Us  
