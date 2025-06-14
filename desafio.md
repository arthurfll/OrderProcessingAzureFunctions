
# Teste Técnico – Backend Pleno com Azure Functions

### Cenário:

Você está criando um **módulo de processamento de pedidos online** para uma empresa de e-commerce. Esse módulo deve ser totalmente serverless, rodando dentro de um **Function App** na Azure.

---

## Descrição Geral do Problema:

A equipe de frontend vai enviar pedidos para uma fila. Depois disso, o backend deve:

1. Processar o pedido assim que ele for colocado na fila
2. Salvar os dados do pedido em um banco (Cosmos DB, Table Storage ou outro que achar adequado)
3. Notificar o cliente por e-mail quando o pedido for processado
4. Expor um endpoint HTTP para consulta do status de um pedido específico


## Requisitos Detalhados:

### **1. Recebimento de Pedido (Trigger 1)**

* **Origem:** Uma fila (pode ser Azure Queue Storage ou Service Bus Queue)
* **Conteúdo:** JSON com os campos:

json
{
  "orderId": "12345",
  "customerEmail": "cliente@exemplo.com",
  "totalAmount": 199.90,
  "items": [
    {"productId": "A1", "quantity": 2},
    {"productId": "B3", "quantity": 1}
  ]
}


* Tarefa: Persistir o pedido e mudar o status para "Processado"



### **2. Persistência (Binding 1)**

* **Destino:** Banco de dados a escolha do candidato
* **Opções válidas:** Cosmos DB, Table Storage, ou qualquer outro serviço PaaS da Azure com binding disponível



### **3. Notificação por E-mail (Trigger 2 + Output Binding)**

* **Disparo:** Após o pedido ser processado
* **Tecnologia sugerida:** Azure SendGrid binding ou qualquer outro serviço de e-mail integrado via Output Binding



### **4. Consulta de Status (Trigger 3)**

* **Requisito:** Criar uma Function HTTP para consultar o status de um pedido
* **Exemplo de chamada:**
  `GET /api/orderstatus?orderId=12345`
* **Resposta esperada:** JSON com o status atual



## 🎯 O ponto chave:

* O candidato **não pode usar apenas HTTP trigger**
* Ele deve combinar pelo menos **3 tipos diferentes de trigger/output binding**:

  * Exemplo de combinação válida: Queue Trigger + Cosmos DB Output Binding + SendGrid Output Binding + HTTP Trigger



## 🧪 Diferenciais:

* Uso de **Durable Functions** (não obrigatório, mas conta ponto extra)
* Uso de **Application Settings para configurações sensíveis (ex: connection strings)**
* Tratamento de erros e DLQ (Dead Letter Queue)
* Testes de unidade (mock de bindings)
* Documentação breve no README explicando decisões de design (ex: porque escolheu tal trigger ou binding)



## ⏱️ Entrega:

* Prazo sugerido: **48 horas**
* Entrega via repositório Git (GitHub ou Azure DevOps)
* Inclua um pequeno README com:

  * Setup
  * Como testar




