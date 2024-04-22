## Documentação para integração via Webhook com o Sellflux.

​
O SellFlux oferece uma interface de integração simplificada para que outras plataformas possam se integrar eficientemente através de webhooks. Este guia fornecerá todas as informações necessárias para configurar e enviar dados para o SellFlux, garantindo uma integração suave e eficaz.

### Configuração do Webhook

Para iniciar a integração via Webhook com o SellFlux, você deve configurar o envio de dados em formato JSON para o endpoint especificado, utilizando o método POST. Certifique-se de incluir o cabeçalho adequado:
```
Content-Type: application/json
```
A URL do endpoint pode ser encontrada dentro do Dashboard do SellFlux, na aba Integrações, criando uma nova integração e copiando o link do tipo "SellFlux".

### Estrutura de Dados

O JSON enviado deve conter as seguintes propriedades, com os seus respectivos valores:

| Campo            | Tipo                  | Exemplo                             | Descrição                                                   |
|------------------|-----------------------|-------------------------------------|-------------------------------------------------------------|
| name             | String                | "sellflux"                          | Nome do lead.                                               |
| email            | String                | "exemplo@sellflux.com"              | Email do lead.                                              |
| phone            | String                | "(99) 99999-9999"                   | Telefone do lead.                                           |
| gateway          | String                | "sellflux"                          | Nome da plataforma de origem.                               |
| transaction_id   | Integer               | 123456                              | Identificador único da transação.                           |
| offer_id         | String                | "123"                               | Identificador da oferta.                                    |
| status           | String                | "cancelado"                         | Status da transação (veja tabela de status abaixo).         |
| payment_date     | DateTime (String)     | "2023-01-25T09:06:50.641815-03"     | Data e hora do pagamento.                                   |
| url              | String                | "https://www.exemplo.com"           | URL para pagamento (boleto, pix).                           |
| payment_method   | String                | "cartao-credito"                    | Método de pagamento utilizado (veja tabela de tipos abaixo).|
| expiration_date  | DateTime - String     | "2023-01-25T09:06:50.641815-03"     | Data de vencimento do pagamento.                            |
| product_id       | String                | "12345"                             | Identificador do produto vendido.                           |
| product_name     | String                | "Exemplo de produto"                | Nome do produto vendido.                                    |
| transaction_value| String                | "299"                               | Valor da transação.                                         |
| ip               | String                | "111.111.11.111"                    | IP do lead.                                                 |
| tags             | Array (String)        | ["gerou-boleto", "comprou-produto"] | Tags que devem ser adicionadas ao lead.                     |
| remove_tags      | Array (String)        | ["pagamento-expirado", "sair"]      | Tags que devem ser removidas do lead.                       |

### Tipos de Pagamentos

Os métodos de pagamento que podem ser reportados ao SellFlux incluem:

| Método de pagamento | Descrição                       |
|---------------------|---------------------------------|
| cartao-credito      | Transação com cartão de crédito |
| pix                 | Transação via PIX               |
| boleto              | Pagamento por boleto bancário   |

### Status de Transações

Os status das transações compreendem:

| Status              | Descrição                               |
|---------------------|-----------------------------------------|
| compra-realizada    | Pagamento recebido e produto reservado  |
| cancelado           | Pedido cancelado por falha no pagamento |
| estornou            | Transação estornada                     |
| disputando          | Disputa aberta pelo comprador           |
| aguardando-pagamento| Esperando conclusão do pagamento        |
| abandonou-carrinho  | Carrinho abandonado pelo comprador      |

### Exemplo de Payload JSON

```json
{
  "name": "sellflux",
  "email": "exemplo@sellflux.com",
  "phone": "(99) 99999-9999",
  "gateway": "sellflux",
  "transaction_id": 123456,
  "offer_id": "123",
  "status": "cancelado",
  "payment_date": "2023-01-25T09:06:50.641815-03",
  "url": "https://www.exemplo.com",
  "payment_method": "cartao-credito",
  "expiration_date": "2023-01-25T09:06:50.641815-03",
  "product_id": "12345",
  "product_name": "Exemplo de produto",
  "transaction_value": "299",
  "ip": "111.111.11.111",
  "tags": ["gerou-boleto", "comprou-produto"],
  "remove_tags": ["pagamento-expirado", "sair"]
}
```

Ao seguir estas diretrizes, sua plataforma poderá se integrar com o SellFlux de maneira eficiente e eficaz, maximizando o potencial de automação e controle de transações.
