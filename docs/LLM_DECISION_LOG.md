# Decisão Técnica: Escolha do LLM / Technical Decision: Choosing an LLM

**Data:** 26/10/2025  
**Autor:** Leandro C. Azambuja  
**Projeto:** Forever Us – Sistema de Legado Digital e Simulação de Personalidade  

---

## Contexto / Context
O projeto **Forever Us** tem como objetivo criar um sistema de legado digital capaz de representar e preservar aspectos da personalidade humana por meio de interações naturais em linguagem.  
Para atingir esse propósito, é essencial escolher um **Modelo de Linguagem (LLM)** que ofereça robustez cognitiva, consistência narrativa e espaço para evolução técnica a longo prazo.

Após análise comparativa e prática, foram considerados três modelos de código aberto: **Mistral 7B**, **Phi-3 Mini (3.8 B)** e **Gemma 2B/7B**.  
A decisão final foi pelo **Mistral 7B**, em virtude de seu desempenho superior e equilíbrio entre poder de raciocínio e liberdade de uso.

---

## Modelos Avaliados / Models Evaluated

|           Critério            |                           Mistral 7B                    |          Phi-3 Mini (3.8 B)      |                   Gemma 7B                  |
|-------------------------------|---------------------------------------------------------|----------------------------------|---------------------------------------------|
| **Desempenho geral**          | **Excelente**, comparável a modelos de 13 B+ parâmetros | Bom desempenho para o tamanho    | Regular a bom, estável mas menos expressivo |
| **Custo de execução**         | Médio – requer GPU ou cloud moderada                    | Baixo – roda em hardware leve    | Médio – otimizado para GCP                  |
| **Tamanho do modelo**         | 7 bilhões de parâmetros                                 | 3.8 bilhões de parâmetros        | 7 bilhões de parâmetros                     |
| **Licenciamento**             | **Apache 2.0** (aberto e comercialmente seguro)         | MIT (também aberto)              | Open Weights (restrições de uso)            |
| **Facilidade de fine-tuning** | **Alta**, com forte suporte e comunidade                | Alta, bom para instruções curtas | Média                                       |
| **Tamanho de contexto**       | Médio (~8 K tokens)                                     | **Excelente (128 K tokens)**     | Médio (~8 K tokens)                         |
| **Adequação à prototipagem**  | Boa                                                     | Excelente                        | Boa                                         |

---

## Fundamentação dos Critérios / Justification of the Criteria

### Desempenho geral / Overall performance
O **Mistral 7B** se destaca por oferecer desempenho de nível superior mesmo com apenas 7 bilhões de parâmetros. Ele supera o LLaMA 2 13B em benchmarks públicos, mantendo coerência, criatividade e precisão em respostas complexas.  
O **Phi-3 Mini**, embora eficiente, ainda apresenta limitações perceptíveis em tarefas de raciocínio encadeado ou respostas com maior contexto emocional.  
O **Gemma 7B**, por sua vez, tem foco em estabilidade, mas carece de nuance e expressividade, pontos essenciais para o *Forever Us*.

### Custo de execução / Cost of execution
Embora o **Mistral 7B** exija maior poder computacional, o custo é considerado **moderado e proporcional ao ganho de qualidade**.  
Essa escolha representa um investimento em robustez: a base cognitiva mais forte reduzirá retrabalho, refinamentos excessivos e dependência de ajustes futuros.  
O **Phi-3 Mini** ainda é vantajoso financeiramente, mas seu desempenho inferior em contextos complexos o torna mais adequado a protótipos, não à fundação de um sistema de legado.  
O **Gemma 7B** mantém custos semelhantes ao Mistral, porém com menor documentação comunitária.

### Tamanho do modelo / Model size
A faixa de **7 bilhões de parâmetros** é um equilíbrio sólido entre capacidade de raciocínio e viabilidade operacional.  
O Mistral 7B entrega uma performance comparável a modelos significativamente maiores, tornando-se uma escolha estratégica: potente o suficiente para expressar nuance e emoção, mas ainda possível de escalar em cloud de médio porte.  
Modelos menores, como o Phi-3 Mini, sacrificam profundidade para manter leveza.

### Licenciamento / Licensing
O licenciamento **Apache 2.0** do Mistral 7B oferece **segurança jurídica e comercial**, algo fundamental para um projeto que poderá futuramente ter monetização, integração com APIs ou distribuição aberta.  
A licença MIT do Phi-3 também é ampla, mas sua dependência do ecossistema Microsoft cria um laço indireto.  
Já a Gemma, apesar de aberta, está sujeita a termos adicionais da Google, o que pode restringir usos comerciais mais amplos.

### Facilidade de fine-tuning / Easy fine-tuning
O **Mistral 7B** possui uma das comunidades mais ativas do mundo open source em 2025, com excelente suporte para fine-tuning e quantização.  
Sua arquitetura moderna (Grouped Query Attention + Sliding Window) facilita ajustes de comportamento, tornando o modelo ideal para personalização de estilo, tom e emoção — características centrais do *Forever Us*.  
O Phi-3 Mini também é acessível, mas voltado a instruções curtas. O Gemma 7B, por outro lado, tem menos material prático de treinamento disponível.

### Tamanho de contexto / Context size
O **Phi-3 Mini** vence em contexto bruto (até 128 K tokens), mas o **Mistral 7B** compensa com **melhor compressão de contexto e consistência narrativa**: mesmo com 8 K tokens, mantém coerência de diálogo superior.  
Além disso, há versões otimizadas e quantizadas do Mistral que suportam contextos ampliados via extensão ou memória externa (RAG), atendendo bem o caso de uso do *Forever Us*.

### Adequação à prototipagem
O Mistral 7B equilibra custo e desempenho, permitindo criar protótipos funcionais e, ao mesmo tempo, manter o mesmo modelo na versão produtiva.  
Essa continuidade técnica evita migrações entre versões e reforça a maturidade arquitetural do projeto.  
O Phi-3 Mini continua sendo uma excelente ferramenta de apoio para testes rápidos, mas o Mistral será a base de longo prazo.

---

## Decisão Final / Final Decision
Optou-se por adotar o **Mistral 7B** como modelo principal do projeto *Forever Us*, priorizando robustez, estabilidade e liberdade jurídica.

> **Justificativa:** o Mistral 7B entrega a melhor relação entre poder cognitivo, clareza contextual e flexibilidade de uso comercial.  
> Sua arquitetura moderna, desempenho superior e ampla compatibilidade tornam-no ideal para sustentar a identidade digital persistente proposta pelo projeto.  
> Ainda que demande mais recursos, a robustez do modelo reduz riscos futuros e assegura a longevidade técnica da solução.

---

## Próximos Passos / Next Steps
1. Implementar o **Mistral 7B** em ambiente local (quantizado) para testes iniciais de coerência e retenção.  
2. Avaliar custos de execução em nuvem (AWS, GCP, Azure) e definir plano de escalabilidade.  
3. Registrar métricas de desempenho e comportamento conversacional.  
4. Mapear estratégias de memória estendida (RAG, vector DB) para evolução do sistema.  
5. Revisar esta decisão a cada marco do projeto.

---

## Estratégia de Implementação Inicial / Initial Implementation Strategy

Para balancear custo e performance no início, usaremos:
- Mistral 7B quantizado (4-bit)** para testes iniciais
- LoRA** para fine-tuning eficiente com poucos dados
- AWS Lambda + GPU apenas para inferência crítica

---

## Métricas de Validação / Validation Metrics

A decisão será considerada acertada se atingirmos:
- [ ] 85%+ de coerência em testes de personalidade
- [ ] Custo inferência < $0.01 por interação  
- [ ] Fine-tuning concluído em < 48h

---

> _“Em tecnologia, robustez é a melhor forma de empatia com o futuro.”_  
> — L.C. Azambuja
