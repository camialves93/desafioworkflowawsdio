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

---

