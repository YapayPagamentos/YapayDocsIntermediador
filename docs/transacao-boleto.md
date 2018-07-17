# Boleto

Também é dispobilizada a funcionalidade de pagamentos com o meio de pagamento Boleto pela API de Transação. É de extrema importância a utilização do nosso fingerprint, abaixo você verá uma explicação mais detalhada sobre isso.

Você pode visualizar os IDs para as formas de pagamento nas nossa <a href="/#/tabelas?id=tabela-3-formas-de-pagamento">Tabela Auxiliar 3 - Formas de Pagamento</a>

Basta você alterar o nó payment para:

```javascript
	    "payment":{  
	       "payment_method_id":"6"
	    }
```	    

No parâmetro `payment[billet_date_expiration]` você pode enviar a data de vencimento do boleto, caso não queira utilizar a padrão das contas Yapay.

Adicionando no nó payment:

```javascript
      "payment":{  
         "payment_method_id":"6",
         "billet_date_expiration": "15/03/2018"
      }
```

## Enviando uma transação


Para esta integração, deverá ser feito <span class="post">POST</span> uso da API a seguir:

| Endereço para Integração                                                                              |
|--------------------------|----------------------------------------------------------------------------|
| Ambiente de Testes       | https://api.intermediador.sandbox.yapay.com.br/api/v3/transactions/payment |
| Ambiente de Produção     | https://api.intermediador.yapay.com.br/api/v3/transactions/payment |
| Protocolo                | Rest/HTTP                                                                  |

Abaixo você consegue visualizar um exemplo em cURL da criação de uma Transação em Boleto:


> **Exemplo de criação de Transação com Boleto**

```bash
    curl  --request POST \
          --url 'https://api.intermediador.sandbox.yapay.com.br/api/v3/transactions/payment' \
          --header 'Content-Type: application/json' \
          --data '{  
              "token_account":"SEU_TOKEN_AQUI",
              "customer":{  
                "contacts":[  
                  {  
                    "type_contact":"H",
                    "number_contact":"1133221122"
                  },
                  {  
                    "type_contact":"M",
                    "number_contact":"11999999999"
                  }
                ],
                "addresses":[  
                  {  
                    "type_address":"B",
                    "postal_code":"17000-000",
                    "street":"Av Esmeralda",
                    "number":"1001",
                    "completion":"A",
                    "neighborhood":"Jd Esmeralda",
                    "city":"Marilia",
                    "state":"SP"
                  }
                ],
                "name":"Stephen Strange",
                "birth_date":"21/05/1941",
                "cpf":"50235335142",
                "email":"stephen.strange@avengers.com"
              },
              "transaction_product":[  
                {  
                  "description":"Camiseta Tony Stark",
                  "quantity":"1",
                  "price_unit":"130.00",
                  "code":"1",
                  "sku_code":"0001",
                  "extra":"Informação Extra"
                }
              ],
              "transaction":{  
                "available_payment_methods":"2,3,4,5,6,7,14,15,16,18,19,21,22,23",
                "customer_ip":"127.0.0.1",
                "shipping_type":"Sedex",
                "shipping_price":"12",
                "price_discount":"",
                "url_notification":"http://www.loja.com.br/notificacao",
                "free":"Campo Livre"
              },
              "payment":{  
                "payment_method_id":"6"
              }
            }'

```



> Resposta da API

A API de Transações retorna a resposta em JSON. Observe que no retorno você recebe dentro do nó payment o campo `url_payment`, com esse campo você pode fazer o redirecionamento para o cliente realizar o pagamento. 

Exemplo de resposta com sucesso baseando no envio do exemplo acima:


```javascript
{
    "message_response": {
        "message": "success"
    },
    "data_response": {
        "transaction": {
            "order_number": "79690",
            "free": "Campo Livre",
            "transaction_id": 79690,
            "status_name": "Aprovada",
            "status_id": 6,
            "token_transaction": "cb22c716c80ddbaa16f8b8dbc49302a2",
            "payment": {
                "price_payment": "142.0",
                "price_original": "142.0",
                "payment_response": "",
                "url_payment": "https://tc.intermediador.sandbox.yapay.com.br/payment/billet/fc0579d4217be829b06755078e26a493",
                "split": 3,
                "payment_method_id": 6,
                "payment_method_name": "Boleto Bancário",
                "linha_digitavel": "123123123123123131232131232131313211231321321"
            },
            "customer": {
                "name": "Stephen Strange",
                "company_name": "",
                "trade_name": "",
                "cnpj": ""
            }
        }
    }
}
```




