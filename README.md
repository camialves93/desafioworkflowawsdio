# desafioworkflowawsdio
Workflow do AWS Step Functions
# AWS Step Functions – Estudo Prático e Anotações

Este repositório foi criado com o objetivo de **documentar o processo de aprendizado e prática com AWS Step Functions**, abordando a orquestração de múltiplos serviços da AWS, automação de fluxos e boas práticas de implementação.

O projeto simula um **fluxo de execução serverless**, integrando Lambda, ECS, DynamoDB e SNS, com controle de lógica e execução paralela via Step Functions.

### Fluxo da State Machine

1. **Lambda Invoke** → executa uma função Lambda inicial, responsável por processar os dados de entrada e definir condições de negócio.  
2. **Choice State** → toma decisões baseadas em parâmetros retornados pela Lambda.  
   - Caso **Regra #1** seja satisfeita, o fluxo segue para a execução **paralela de tarefas ECS**.
   - Caso contrário (**Default**), o fluxo segue para **armazenar dados no DynamoDB** e **enviar notificação via SNS**.
3. **Parallel State** → executa múltiplas tarefas ECS simultaneamente para otimizar o tempo de processamento.
4. **DynamoDB PutItem** → grava resultados no banco de dados.
5. **SNS Publish** → envia uma mensagem ou alerta de conclusão do processo.
6. **End** → encerra o fluxo.

## ☁️ Serviços AWS Utilizados

| Serviço AWS | Função no Projeto | Observações |
|--------------|------------------|--------------|
| **AWS Lambda** | Processar lógica inicial e preparar entrada | Responsável pela decisão inicial |
| **Amazon ECS** | Executar containers em paralelo | Reduz tempo de execução total |
| **Amazon DynamoDB** | Persistir dados e resultados | Ideal para armazenamento NoSQL escalável |
| **Amazon SNS** | Envio de notificações automáticas | Integração simples com e-mails, filas ou mensagens |
| **AWS Step Functions** | Orquestração do fluxo de execução | Permite controle, monitoramento e paralelismo |

---

## Aprendizados e Insights

###  Orquestração e Controle de Fluxo
- Step Functions simplifica a **coordenação de múltiplos serviços** AWS sem a necessidade de código complexo.
- O uso de **Choice States** permite criar fluxos **dinâmicos e condicionais**, baseados em parâmetros de entrada.
- O **Parallel State** é uma poderosa ferramenta para **reduzir o tempo total de execução**, executando subtarefas simultaneamente.

###  Boas Práticas Implementadas
- **Uso de Retry e Catch** para tornar o fluxo resiliente a falhas temporárias.
- **Separação de responsabilidades**: cada Lambda e ECS Task executa uma função clara e isolada.
- **Monitoramento e Logs** via **CloudWatch** para rastrear falhas e desempenho.
- **Versionamento do State Machine JSON** para controle de alterações e auditoria.

###  Desafios Encontrados
- Sincronização de dados entre estados paralelos.
- Gerenciamento de permissões IAM adequadas para cada serviço.
- Manutenção de rastreabilidade e logging em execuções complexas.

###  Resultados Alcançados
- Implementação funcional de um **workflow automatizado** e **paralelo**.
- Maior compreensão sobre **design de sistemas serverless**.
- Criação de uma base sólida para **projetos futuros com automação AWS**.

---

## Conclusão

Este estudo demonstrou na prática como **Step Functions podem integrar múltiplos serviços AWS** para criar pipelines complexos de maneira simples, escalável e resiliente.  
A prática reforçou a importância de **arquiteturas orientadas a eventos**, **execuções paralelas** e **observabilidade** em sistemas distribuídos.

---

## Próximos Passos

- Adicionar logs detalhados no CloudWatch.
- Implementar tratamento de exceções mais granular.
- Expandir o fluxo com chamadas assíncronas para APIs externas.
- Criar testes automatizados para Lambda e ECS Tasks.


