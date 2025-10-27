# 🧠 AWS Infrastructure Decision Log – Projeto ForeverUS

**Versão:** 1.0  
**Data:** Outubro / 2025  
**Responsável:** Equipe ForeverUS – Programa Restart / Escola da Nuvem  
**Objetivo:** Documentar as decisões de infraestrutura AWS adotadas para o MVP (LLM) e para a versão completa futura do projeto.

---

## 🔹 1. MVP – LLM (Versão Inicial e Econômica)

### 1.1 AWS S3 (Simple Storage Service)
**Função:**  
Hospedagem do frontend (arquivos estáticos – HTML, CSS, JS).  

**Justificativa:**  
Serviço de baixo custo, altamente disponível e sem necessidade de servidor dedicado.  
Ideal para aplicações estáticas e com integração futura via CloudFront.

---

### 1.2 AWS Elastic Beanstalk
**Função:**  
Hospedar e gerenciar o backend (API da aplicação).  

**Justificativa:**  
Automatiza a criação e gestão da infraestrutura (EC2, Load Balancer, Auto Scaling e CloudWatch).  
Permite implantar o backend de forma simples, sem configurar manualmente instâncias.  
Escala automaticamente conforme a demanda e integra facilmente com RDS, S3 e IAM.  
Ideal para o MVP por reduzir a complexidade e manter o foco no código.

---

### 1.3 AWS EC2 (Elastic Compute Cloud)
**Função:**  
Execução da LLM (Mistral 7B quantizado).  

**Justificativa:**  
Utilização de instância GPU do tipo *spot* para reduzir custos.  
Ativada apenas durante testes de inferência, evitando custo contínuo.  
O modelo quantizado (4-bit) reduz o consumo de VRAM e o custo operacional.

---

### 1.4 AWS EBS (Elastic Block Store)
**Função:**  
Armazenar os artefatos e dependências da LLM.  

**Justificativa:**  
Permite desligar a instância EC2 sem perda de dados.  
Cobra apenas pelo armazenamento, mantendo o custo sob controle.

---

### 1.5 AWS Lambda *(opcional)*
**Função:**  
Executar funções pontuais do backend (como controle de requisições ou autenticação).  

**Justificativa:**  
Modelo serverless pago por uso.  
Ideal para lógicas leves entre o frontend e a LLM hospedada.

---

### 1.6 AWS CloudWatch
**Função:**  
Monitoramento e coleta de logs do ambiente (EC2, Lambda e Beanstalk).  

**Justificativa:**  
Permite registrar métricas e desempenho, otimizando uso de créditos e identificando gargalos.

---

### 1.7 AWS Budgets
**Função:**  
Controle de gastos e alertas de uso dos créditos AWS.  

**Justificativa:**  
Envia notificações automáticas quando o uso ultrapassa limites definidos (50%, 80%, 100%).  
Essencial no contexto educacional do programa Restart.

---

### 1.8 AWS DynamoDB *(opcional)*
**Função:**  
Armazenar histórico de conversas e logs leves.  

**Justificativa:**  
Banco NoSQL escalável e de baixo custo.  
Pode ser substituído por armazenamento simples no S3 durante o MVP.

---

### 🔸 Fluxo Simplificado do MVP

[Usuário]
   ↓
[Frontend - S3]
   ↓
[Elastic Beanstalk (API Backend)]
   ↓
[EC2 - Mistral 7B]
   ↓
[Resposta → Frontend]

---
Objetivo: Validar o funcionamento da LLM com simplicidade e custo reduzido.

**2. Arquitetura Completa (Versão Futura do Projeto)**

Essa fase será ativada após a validação do MVP, quando o projeto expandir para multimodalidade (voz, imagem e contexto persistente).

2.1 AWS ECS (Elastic Container Service)

Função:
Orquestrar microserviços (voz, imagem, contexto, etc.).

Justificativa:
Proporciona escalabilidade e isolamento de funções sem múltiplas EC2s.
Facilita manutenção e atualizações modulares.

2.2 AWS RDS (Relational Database Service)

Função:
Armazenar dados estruturados (usuários, histórico e preferências).

Justificativa:
Banco relacional com backups automáticos e alta disponibilidade.
Ideal para quando houver relações complexas entre usuários e contextos.

2.3 AWS CloudFront

Função:
CDN para distribuição global do frontend hospedado no S3.

Justificativa:
Reduz latência e melhora performance em múltiplas regiões.

2.4 AWS SQS (Simple Queue Service)

Função:
Enfileirar requisições de inferência para a LLM.

Justificativa:
Evita sobrecarga do backend e garante ordem no processamento das requisições.

2.5 AWS SNS (Simple Notification Service)

Função:
Enviar notificações automáticas (e-mail, webhook, etc.).

Justificativa:
Facilita comunicação entre serviços e alertas operacionais.

2.6 AWS IAM (Identity and Access Management)

Função:
Controlar permissões e papéis de cada serviço AWS.

Justificativa:
Garante segurança e o princípio do privilégio mínimo.

2.7 AWS Secrets Manager

Função:
Armazenar chaves, tokens e segredos com segurança.

Justificativa:
Evita exposição de credenciais no código-fonte e facilita rotação de chaves.

2.8 AWS Step Functions

Função:
Automatizar fluxos complexos (ligar EC2, processar, desligar, notificar).

Justificativa:
Permite criar rotinas automatizadas sem scripts externos, reduzindo erros humanos.

2.9 AWS SageMaker (ou Amazon Bedrock)

Função:
Hospedar ou treinar versões otimizadas da LLM.

Justificativa:
Elimina a necessidade de gerenciar GPUs manualmente.
Permite upgrade futuro com fine-tuning e integração nativa com APIs AWS.

🔸 Fluxo da Arquitetura Completa
