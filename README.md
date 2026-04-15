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
| currency         | String                | "brl"                               | Tipo da moeda (Real, Dólar, etc...)                         |
| add              | Object                | (veja estrutura abaixo)             | Dados adicionais da transação (endereço, desconto, etc.).   |
| itens            | Array (Object)        | (veja estrutura abaixo)             | Lista de itens da transação.                                |
| shipping_company | String                | "Correios"                          | Empresa de envio/transportadora.                            |
| tracking_id      | String                | "TR123456"                          | Identificador do rastreamento.                              |
| external_id      | String                | "EXT-789"                           | Identificador externo do rastreamento.                      |
| tracking_status  | String                | "em-transporte"                     | Status do rastreamento (ex: enviado, entregue, etc.).       |
| tracking         | String                | "BR123456789BR"                     | Código de rastreamento do envio.                            |
| tracking_url     | String                | "https://rastreio.exemplo.com/BR123"| URL para acompanhar o rastreamento.                         |
| trail_date       | DateTime (String)     | "2023-01-25T09:06:50.641815-03"     | Data do rastreamento/envio.                                 |
| shipping_method  | String                | "sedex"                             | Método de envio utilizado.                                  |

### Estrutura do campo `add`

O campo `add` é um objeto opcional que pode conter informações adicionais da transação:

| Campo            | Tipo                  | Exemplo                             | Descrição                                                   |
|------------------|-----------------------|-------------------------------------|-------------------------------------------------------------|
| address          | String                | "Rua Exemplo, 123"                  | Endereço associado à transação.                             |
| price_discount   | Number                | 50.00                               | Valor de desconto aplicado na transação.                    |

> **Nota:** O campo `add` aceita propriedades adicionais além das listadas acima.

### Estrutura do campo `itens`

O campo `itens` é um array opcional de objetos representando os itens da transação:

| Campo            | Tipo                  | Exemplo                             | Descrição                                                   |
|------------------|-----------------------|-------------------------------------|-------------------------------------------------------------|
| id               | String                | "item-001"                          | Identificador do item.                                      |
| name             | String                | "Camiseta XYZ"                      | Nome do item.                                               |
| quantity         | Number                | 2                                   | Quantidade do item.                                         |
| price            | Number                | 49.90                               | Preço unitário do item.                                     |
| value            | Number                | 99.80                               | Valor total do item (preço x quantidade).                   |
| offset           | Number                | 0                                   | Offset do item.                                             |
| image            | String                | "https://exemplo.com/img.jpg"       | URL da imagem do item.                                      |
| discount         | Number                | 5.00                                | Valor de desconto aplicado ao item.                         |

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

### Tipos de moedas aceitos

Os tipos de moedas compreendem:

| Sigla               | Localidade                              |
|---------------------|-----------------------------------------|
| USD                 | Dólar Americano                         |
| EUR                 | Euro                                    |
| GBP                 | Libra esterlina                         |
| JPY                 | Iene                                    |
| AUD                 | Dólar Australiano                       |
| CHF                 | Franco Suíço                            |
| CAD                 | Dólar Canadense                         |
| CNY                 | Renminbi (Yuan)                         |

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
  "transaction_value": "249",
  "ip": "111.111.11.111",
  "tags": ["gerou-boleto", "comprou-produto"],
  "remove_tags": ["pagamento-expirado", "sair"],
  "currency": "brl",
  "add": {
    "address": "Rua Exemplo, 123",
    "price_discount": 50.00
  },
  "itens": [
    {
      "id": "item-001",
      "name": "Exemplo de produto",
      "quantity": 1,
      "price": 299,
      "value": 299,
      "offset": 0,
      "image": "https://www.exemplo.com/img.jpg",
      "discount": 0
    }
  ],
  "shipping_company": "Correios",
  "tracking_id": "TR123456",
  "external_id": "EXT-789",
  "tracking_status": "em-transporte",
  "tracking": "BR123456789BR",
  "tracking_url": "https://rastreio.exemplo.com/BR123",
  "trail_date": "2023-01-25T09:06:50.641815-03",
  "shipping_method": "sedex"
}
```

Ao seguir estas diretrizes, sua plataforma poderá se integrar com o SellFlux de maneira eficiente e eficaz, maximizando o potencial de automação e controle de transações.
