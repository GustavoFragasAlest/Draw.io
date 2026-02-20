<div align="center">

# 💳 API de Pagamentos — Documentação de Arquitetura

[![Draw.io](https://img.shields.io/badge/Diagrams-Draw.io-orange?logo=diagramsdotnet&logoColor=white)](https://app.diagrams.net)
[![AWS](https://img.shields.io/badge/Cloud-AWS-232F3E?logo=amazonaws&logoColor=white)](https://aws.amazon.com)
[![MCP](https://img.shields.io/badge/AI-MCP%20Enabled-blueviolet?logo=anthropic&logoColor=white)](https://modelcontextprotocol.io)
[![Docs as Code](https://img.shields.io/badge/Docs-as--Code-informational?logo=markdown&logoColor=white)](https://www.writethedocs.org/guide/docs-as-code/)

> Documentação técnica da API de Pagamentos usando a abordagem **Docs-as-Code** com diagramas editáveis diretamente no repositório.

</div>

---

## 📋 Índice

- [Visão Geral](#-visão-geral)
- [Arquitetura Base](#-arquitetura-base)
- [Arquitetura AWS](#-arquitetura-aws-nova-feature)
- [Fluxo de Pagamento](#-fluxo-de-pagamento)
- [Stack Tecnológica](#-stack-tecnológica)
- [Como Editar os Diagramas](#-como-editar-os-diagramas)

---

## 🔭 Visão Geral

Este repositório documenta a arquitetura da **API de Pagamentos** utilizando a abordagem **Docs-as-Code**: os diagramas são arquivos `.drawio.svg` versionados junto ao código-fonte.

Isso significa que:
- ✅ Os diagramas aparecem **renderizados automaticamente** aqui no GitHub
- ✅ Qualquer dev pode **editar visualmente** os blocos abrindo o arquivo no VS Code
- ✅ Toda alteração é **rastreada pelo Git** como qualquer outro arquivo
- ✅ Chega de prints de tela desatualizados na documentação

---

## 🏗 Arquitetura Base

Fluxo simplificado mostrando os três componentes principais do sistema:

![Arquitetura de Pagamento](../arquitetura-pagamento.drawio.svg)

| Componente | Responsabilidade |
|---|---|
| **Usuário** | Origina a requisição de pagamento |
| **Servidor** | Processa e valida a transação |
| **Banco de Dados** | Persiste o estado da transação |

---

## ☁️ Arquitetura AWS — Nova Feature

Diagrama completo da nova infraestrutura na AWS com ícones oficiais, gerado via MCP do Draw.io:

![Nova Arquitetura AWS](./nova-arquitetura.drawio.svg)

### Serviços utilizados

| Serviço | Tipo | Função |
|---|---|---|
| ![](https://img.shields.io/badge/-API%20Gateway-E7157B?logo=amazonaws&logoColor=white) | Gerenciado | Ponto de entrada HTTP da API |
| ![](https://img.shields.io/badge/-Lambda-ED7100?logo=awslambda&logoColor=white) | Serverless | Validação e processamento da transação |
| ![](https://img.shields.io/badge/-DynamoDB-C925D1?logo=amazondynamodb&logoColor=white) | NoSQL | Persistência de transações aprovadas |
| ![](https://img.shields.io/badge/-SQS-E7157B?logo=amazonsqs&logoColor=white) | Queue | Fila de reprocessamento para recusados |

---

## 🔄 Fluxo de Pagamento

```
Cliente
  │
  ▼
API Gateway ──────────────────────┐
  │                               │
  ▼                               │
Lambda Validação                  │
  │                               │
  ├─── ✅ Aprovado ──▶ DynamoDB   │
  │                               │
  └─── ❌ Recusado ──▶ Fila SQS  │
                                  │
         (reprocessamento) ◀──────┘
```

1. O **Cliente** envia a requisição de pagamento
2. O **API Gateway** autentica e roteia para a Lambda
3. A **Lambda de Validação** aplica as regras de negócio
4. Se **aprovado** → transação gravada no **DynamoDB**
5. Se **recusado** → mensagem enfileirada no **SQS** para retry automático

---

## 🛠 Stack Tecnológica

| Camada | Tecnologia |
|---|---|
| Diagramas | [Draw.io](https://app.diagrams.net) + `.drawio.svg` |
| IA para geração | [MCP `@drawio/mcp`](https://www.npmjs.com/package/@drawio/mcp) |
| Editor | VS Code + Draw.io Integration |
| Cloud | AWS (API Gateway, Lambda, DynamoDB, SQS) |
| Docs | Markdown + Docs-as-Code |

---

## ✏️ Como Editar os Diagramas

Os arquivos `.drawio.svg` são **totalmente editáveis** sem sair do VS Code:

```bash
# Clone o repositório
git clone <url-do-repo>

# Abra no VS Code
code .
```

1. Navegue até qualquer arquivo `.drawio.svg` no Explorer
2. Clique no arquivo — o editor Draw.io abre automaticamente
3. Arraste novos componentes, edite rótulos, reorganize as setas
4. `Ctrl+S` para salvar — o arquivo atualiza o SVG e o diagrama simultaneamente
5. Commit normalmente com `git commit`

> 💡 **Dica:** Para gerar novos diagramas via IA, o servidor MCP `@drawio/mcp` já está configurado em `.vscode/mcp.json`.

---

<div align="center">

Feito com ❤️ usando **Docs-as-Code** + **Draw.io** + **AWS**

</div>
