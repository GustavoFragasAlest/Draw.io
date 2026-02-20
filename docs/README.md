# Documentação da API de Pagamentos

Abaixo está o fluxo de arquitetura desenhado para a nova feature:

![Arquitetura de Pagamento](../arquitetura-pagamento.drawio.svg)

Como você pode ver, o cliente se comunica direto com nosso gateway...

---

## Nova Arquitetura AWS (Migração Mermaid → Draw.io)

Abaixo está o diagrama convertido do Mermaid para Draw.io com ícones oficiais AWS:

![Nova Arquitetura AWS](./nova-arquitetura.drawio.svg)

### Fluxo:
1. **Cliente** envia requisição ao **API Gateway**
2. **API Gateway** encaminha para a **Lambda de Validação**
3. Se **Aprovado** → grava no **DynamoDB**
4. Se **Recusado** → enfileira no **SQS** para reprocessamento
