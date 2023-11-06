## Documentação Webhook Sellflux.

​
Uma maneira fácil de integrar sua aplicação com o nosso sistema de automação.
​

### Propriedade (Verifique na tabela abaixo os tipos aceito)

​
Propriedades que você deve passar.
​
O metodo é do tipo POST e os dados devem ser passado em formato Content-Type: application/json.
​
| status | Exemplo | Descrição |
| ----------------- | ----------------------------------- | ------------------------------------------------ |
| name | 'sellflux' | Nome do lead |
| email | 'exemplo@sellflux.com' | Email do lead |
| phone | '(99) 99999-9999' | Telefone do lead |
| gateway | 'sellflux' | Nome da sua plataforma |
| transaction_id | 123456 | Id da transação, este id da transação é `único`. |
| status | 'cancelado' | O status da sua compra |
| payment_date | '2023-01-25 09:06:50.641815-03' | Data que foi pago a compra |
| url | 'https://www.exemplo.com' | Link do boleto ou pix da compra |
| payment_method | 'cartao-credito' | Método de pagamento utilizado na compra |
| expiration_date | '2023-01-25 09:06:50.641815-03' | Data de expiração do pagamento |
| product_id | '12345' | Id do produto vendido |
| product_name | 'Exemplo de produto' | Nome do produto |
| transaction_value | '299' | Valor da compra |
| tags | ['gerou-boleto', 'comprou-produto'] | Tags para adicionar aos leads |
| remove_tags | ['pagamento-expirado', 'sair'] | Tags para remover dos leads |
​

### Tipos de Pagamentos

​
Tipo de pagamentos Disponíveis para você.
​
| payment | Descrição |
| -------------- | ------------------------------------- |
| cartao-credito | Transação feita com cartão de crédito |
| pix | Transação feita por pix |
| boleto | Transação feita por boleto |
​

### Status

​
| status | Nome | Descrição |
| -------------------- | -------------------------------- | --------------------------------------------------------------------- |
| compra-realizada | Pago | Já está pago e em breve entrará em separação(caso físico) |
| cancelado | Cancelado | O pedido foi cancelado por algum motivo como pagamento recusado |
| estornou | Estornou | O pedido foi estornado por algum motivo como arrependimento da compra |
| disputando | Em disputa | O pedido está em disputa, comprador quer o dinheiro de volta |
| aguardando-pagamento | Reservado - Aguardando Pagamento | O pedido foi reservado e está aguardando pagamento |
| abandonou-carrinho | Carrinho Perdido | Carrinho abandonado |
​

### Exemplo JSON

​

```json
{
  "name": "sellflux",
  "email": "exemplo@sellflux.com",
  "phone": "(99) 99999-9999",
  "gateway": "sellflux",
  "transaction_id": 123456,
  "status": "cancelado",
  "payment_date": "2023-01-25 09:06:50.641815-03",
  "url": "https://www.exemplo.com",
  "payment_method": "cartao-credito",
  "expiration_date": "2023-01-25 09:06:50.641815-03",
  "product_id": "12345",
  "product_name": "Exemplo de produto",
  "transaction_value": "299",
  "tags": ["gerou-boleto", "comprou-produto"],
  "remove_tags": ["pagamento-expirado", "sair"]
}
```
