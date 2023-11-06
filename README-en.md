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
​

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

### Example JSON

​

```json
{
  "name": "sellflux",
  "email": "example@sellflux.com",
  "phone": "(99) 99999-9999",
  "gateway": "sellflux",
  "transaction_id": 123456,
  "status": "cancelado",
  "payment_date": "2023-01-25 09:06:50.641815-03",
  "url": "https://www.example.com",
  "payment_method": "cartao-credito",
  "expiration_date": "2023-01-25 09:06:50.641815-03",
  "product_id": "12345",
  "product_name": "example product",
  "transaction_value": "299",
  "tags": ["gerou-boleto", "comprou-produto"],
  "remove_tags": ["pagamento-expirado", "sair"]
}
```
