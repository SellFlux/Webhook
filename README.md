## Documentação Webhook Sellflux.

Uma maneira fácil de integrar sua aplicação com o nosso sistema de automação.

### Propriedade (Verifique na tabela abaixo os tipos aceito)

Propriedades que você deve passar.

| status                 | Exemplo                                 | Descrição                                                                                    |
| -----------------------| --------------------------------------- | -------------------------------------------------------------------------------------------- |
| nome                   | 'sellflux'                              | Nome do lead                              									                  |
| email                  | 'exemplo@sellflux.com'                  | Email do lead                          									                  |
| telefone               | '(99) 99999-9999'                       | Telefone do lead                              									              |
| gateway                | 'sellflux'                              | Nome da sua plataforma                              									      |
| transaction_id         | '123456'                                | Id da transação, este id da transação é `único`.                              				  |
| status                 | 'cancelado'                             | O status da sua compra                         										      |
| payment_date           | '01/01/2001'                            | Data que foi pago a compra                                 							      |
| url                    | 'https://www.exemplo.com'               | Link do boleto ou pix da compra                                       						  |
| payment_method         | 'cartao-credito'                        | Método de pagamento utilizado na compra                                                      |
| expiration_date        | '02/02/2002'                            | Data de expiração do pagamento                                                               |
| product_id             | '12345'                                 | Id do produto vendido                                                                        |
| product_name           | 'Exemplo de produto'                    | Nome do produto                                                                 			  |
| transaction_value      | '299'                                   | Valor da compra                                                                              |

### Tipos de Pagamentos

Tipo de pagamentos Disponíveis para você.

| payment                 | Descrição                                  |
| -----------------------| ------------------------------------------ |
| cartao-credito         | Transação feita com cartão de crédito      |
| pix                    | Transação feita por pix                    |
| boleto                 | Transação feita por boleto                 |

### Status


| status                 | Nome                                    | Descrição                                                                                    |
| -----------------------| --------------------------------------- | -------------------------------------------------------------------------------------------- |
| compra-realizada       | Pago                                    | Já está pago e em breve entrará em separação(caso físico)                                    |
| cancelado              | Cancelado                               | O pedido foi cancelado por algum motivo como pagamento recusado                              |
| estornou               | Estornou                                | O pedido foi estornado por algum motivo como arrependimento da compra                        |
| disputando             | Em disputa                              | O pedido está em disputa, comprador quer o dinheiro de volta                                 |
| aguardando-pagamento   | Reservado - Aguardando Pagamento        | O pedido foi reservado e está aguardando pagamento                                           |
| abandonou-carrinho     | Carrinho Perdido | Carrinho abandonado  | Cliente abandonou o carrinho                                                                 |                                                       