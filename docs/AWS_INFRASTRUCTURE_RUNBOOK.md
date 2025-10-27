# 🧠 AWS Infrastructure Decision Log – Projeto ForeverUS

**Versão:** 1.1  
**Data:** Outubro / 2025  
**Responsável:** Equipe ForeverUS – Programa Restart / Escola da Nuvem  
**Objetivo:** Documentar as decisões de infraestrutura AWS adotadas para o MVP (LLM) e versão completa futura, com foco em economia e uso racional de créditos.

---

## 🎯 Princípios de Arquitetura

- **Custo-efetividade:** Priorizar serviços serverless e instâncias spot/sob demanda
- **Simplicidade:** Manter stack enxuta para MVP
- **Escalabilidade:** Planejar para crescimento sem custo inicial desnecessário
- **Educacional:** Alinhar com boas práticas do programa Escola da Nuvem

---

## 🔹 MVP – Arquitetura Econômica (Fase 1)

### 1.1 **S3 (Amazon Simple Storage Service)**
**Função:** Hospedagem do frontend estático (HTML, CSS, JS)  
**Justificativa:** Baixo custo, alta disponibilidade, integração nativa com CloudFront. Ideal para aplicações estáticas.

### 1.2 **Elastic Beanstalk**
**Função:** Hospedagem e gerenciamento automático do backend (API + aplicação)  
**Justificativa:** 
- Simplifica deploy e gerenciamento comparado à EC2 pura
- Automatiza scaling, load balancing e monitoring
- Ideal para contexto educacional - foca no código, não na infra
- Custo eficiente: paga apenas pelos recursos subjacentes (EC2, ELB)

### 1.3 **API Gateway** 
**Função:** Ponto de entrada para APIs adicionais e integrações  
**Justificativa:** HTTP API é econômico e suficiente para integrações específicas com serviços externos.

### 1.4 **Lambda**
**Função:** Funções específicas e event-driven  
**Justificativa:** Serverless para tarefas pontuais (validações, processamentos leves). Paga-se apenas pelo uso.

### 1.5 **EC2 GPU (Spot Instance)**
**Função:** Execução do Mistral 7B quantizado  
**Justificativa:** 
- Instância spot reduz custos em ~70%
- Ativação sob demanda durante desenvolvimento/testes
- Modelo 4-bit otimiza uso de VRAM

### 1.6 **EBS (Elastic Block Store)**
**Função:** Storage persistente para a EC2 GPU  
**Justificativa:** Permite desligar instância sem perder ambiente configurado.

### 1.7 **CloudWatch + Budgets**
**Função:** Monitoramento e controle de custos  
**Justificativa:** Essencial para gerenciar créditos educacionais com alertas automáticos.

---

## 🔸 Arquitetura Completa (Fase 2 - Visão Futura)

### 2.1 **CloudFront**
**Função:** CDN para frontend estático  
**Justificativa:** Melhora performance global e reduz latência.

### 2.2 **RDS (PostgreSQL)**
**Função:** Banco relacional para dados estruturados  
**Justificativa:** Backup automático, alta disponibilidade, ideal para dados de usuários e histórico.

### 2.3 **DynamoDB**
**Função:** Banco NoSQL para sessões e dados semi-estruturados  
**Justificativa:** Baixa latência, custo variável por uso.

### 2.4 **SQS + SNS**
**Função:** Filas e notificações para processamento assíncrono  
**Justificativa:** Desacopla serviços e melhora resiliência.

### 2.5 **ECS/Fargate**
**Função:** Containers para microserviços especializados  
**Justificativa:** Isolamento de funcionalidades (voz, imagem, etc.) com melhor controle de recursos.

---

## 📊 Resumo Visual do MVP

[Usuário]
↓
[S3 + CloudFront] → Frontend Estático
↓
[Elastic Beanstalk] → Backend (API + Aplicação)
↓
[Lambda] → Funções Específicas
↓
[EC2 GPU Spot] → LLM Mistral 7B
↓
[EBS] → Persistência do Modelo
↓
[CloudWatch] → Monitoramento & Budgets


---

## 💡 Estratégia de Custos

1. **Instâncias Spot:** Para workloads de desenvolvimento/teste
2. **Serverless First:** Lambda, S3, API Gateway como padrão
3. **Auto-scaling:** Configurado no Elastic Beanstalk
4. **Budgets:** Alertas em 50%, 80% e 95% dos créditos
5. **Desligamento Automático:** Scripts para EC2 fora do horário comercial

---

## 🚀 Próximos Passos Imediatos

1. **Configurar Elastic Beanstalk** para o backend principal
2. **Implementar S3** para frontend estático  
3. **Preparar instância EC2 GPU spot** para LLM
4. **Configurar CloudWatch Budgets** para controle de custos
5. **Documentar procedimentos** no RUNBOOK operacional

---

**Observação:** Esta arquitetura equilibra simplicidade operacional com custo-efetividade, sendo ideal para o contexto educacional do programa Restart enquanto mantém caminho aberto para expansão futura.

