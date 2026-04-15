## Documentation Webhook Sellflux.

​
An easy way to integrate your application with our automation system.
​

### property (Check the table Below are the accepted types)

​
Properties you must pass.
​
The method is of the type POST and the data must be passed in format Content-Type: application/json.
​
| status | Example | Description |
| ----------------- | ----------------------------------- | ---------------------------------------------- |
| name | 'sellflux' | lead name |
| email | 'example@sellflux.com' | lead email |
| phone | '(99) 99999-9999' | Lead number |
| gateway | 'sellflux' | Name of your platform |
| transaction_id | 123456 | Transaction ID, this transaction ID is unique. |
| status | 'cancelado' | The status of your purchase |
| payment_date | '2023-01-25 09:06:50.641815-03' | Date when the purchase was paid |
| url | 'https://www.example.com' | Payment link for the purchase or Pix |
| payment_method | 'cartao-credito' | Payment method used in the purchase |
| expiration_date | '2023-01-25 09:06:50.641815-03' | Payment expiration date |
| product_id | '12345' | Product ID sold |
| product_name | 'example product' | Product name |
| transaction_value | '299' | Purchase amount/Purchase value |
| tags | ['gerou-boleto', 'comprou-produto'] | Tags to add to the leads |
| remove_tags | ['pagamento-expirado', 'sair'] | Tags to remove from the leads |
| offer_id | '123' | Offer identifier |
| ip | '111.111.11.111' | Lead's IP address |
| currency | 'brl' | Currency type (USD, EUR, BRL, etc.) |
| add | (see structure below) | Additional transaction data (address, discount, etc.) |
| itens | (see structure below) | List of transaction items |
| shipping_company | 'Correios' | Shipping company/carrier |
| tracking_id | 'TR123456' | Tracking identifier |
| external_id | 'EXT-789' | External tracking identifier |
| tracking_status | 'em-transporte' | Tracking status (e.g. enviado, entregue, etc.) |
| tracking | 'BR123456789BR' | Shipment tracking code |
| tracking_url | 'https://tracking.example.com/BR123' | URL to track the shipment |
| trail_date | '2023-01-25 09:06:50.641815-03' | Tracking/shipping date |
| shipping_method | 'sedex' | Shipping method used |
​

### `add` Field Structure

The `add` field is an optional object that may contain additional transaction information:

| Field | Example | Description |
| ----------------- | ----------------------------------- | ---------------------------------------------- |
| address | 'Rua Exemplo, 123' | Address associated with the transaction |
| price_discount | 50.00 | Discount amount applied to the transaction |

> **Note:** The `add` field accepts additional properties beyond those listed above.

### `itens` Field Structure

The `itens` field is an optional array of objects representing the transaction items:

| Field | Example | Description |
| ----------------- | ----------------------------------- | ---------------------------------------------- |
| id | 'item-001' | Item identifier |
| name | 'Example Product' | Item name |
| quantity | 2 | Item quantity |
| price | 49.90 | Item unit price |
| value | 99.80 | Item total value (price x quantity) |
| offset | 0 | Item offset |
| image | 'https://example.com/img.jpg' | Item image URL |
| discount | 5.00 | Discount amount applied to the item |

### Types of Payments

​
Types of payments available to you.
​
| payment | Descrição |
| -------------- | ------------------------------------ |
| cartao-credito | Transaction made with a credit card |
| pix | Transaction made via Pix |
| boleto | Transaction made through a bank slip |
​

### Status

​
| status | Nome | Descrição |
| -------------------- | --------------------------- | ------------------------------------------------------------------------- |
| compra-realizada | Paid | It is already paid and will soon enter the picking process(physical case) |
| cancelado | Canceled | The order has been canceled for some reason, such as payment declined |
| estornou | Refunded | The order was refunded for some reason, such as buyer's remorse |
| disputando | In dispute | The order is in dispute; the buyer wants a refund |
| aguardando-pagamento | Reserved - Awaiting Payment | The order has been reserved and is awaiting payment |
| abandonou-carrinho | Lost Cart | Abandoned cart |
​

### Accepted Currency Types

| Code | Currency |
| ---- | -------- |
| USD | US Dollar |
| EUR | Euro |
| GBP | British Pound |
| JPY | Japanese Yen |
| AUD | Australian Dollar |
| CHF | Swiss Franc |
| CAD | Canadian Dollar |
| CNY | Chinese Yuan (Renminbi) |

### Example JSON

​

```json
{
  "name": "sellflux",
  "email": "example@sellflux.com",
  "phone": "(99) 99999-9999",
  "gateway": "sellflux",
  "transaction_id": 123456,
  "offer_id": "123",
  "status": "cancelado",
  "payment_date": "2023-01-25 09:06:50.641815-03",
  "url": "https://www.example.com",
  "payment_method": "cartao-credito",
  "expiration_date": "2023-01-25 09:06:50.641815-03",
  "product_id": "12345",
  "product_name": "example product",
  "transaction_value": "249",
  "ip": "111.111.11.111",
  "tags": ["gerou-boleto", "comprou-produto"],
  "remove_tags": ["pagamento-expirado", "sair"],
  "currency": "brl",
  "add": {
    "address": "123 Example Street",
    "price_discount": 50.00
  },
  "itens": [
    {
      "id": "item-001",
      "name": "Example product",
      "quantity": 1,
      "price": 299,
      "value": 299,
      "offset": 0,
      "image": "https://www.example.com/img.jpg",
      "discount": 0
    }
  ],
  "shipping_company": "Correios",
  "tracking_id": "TR123456",
  "external_id": "EXT-789",
  "tracking_status": "em-transporte",
  "tracking": "BR123456789BR",
  "tracking_url": "https://tracking.example.com/BR123",
  "trail_date": "2023-01-25 09:06:50.641815-03",
  "shipping_method": "sedex"
}
```
