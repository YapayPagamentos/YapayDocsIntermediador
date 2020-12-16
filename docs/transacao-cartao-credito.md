## Dados do Cartão de Crédito


Uma das funcionalidades do Yapay Intermediador é criação de transações pela API de Transação com o meio de pagamento **Cartão de Crédito**.

É de extrema importância a utilização do nosso Fingerprint, visto que é uma importante ferramenta no processo de análise antifraude das transações criadas em sua loja. Você pode entender mais do sobre o Fingerprint clicando [aqui](https://intermediador.dev.yapay.com.br/#/transacao-fingerprint)

Você pode visualizar os ID's referente as formas de pagamento na nossa <a href="/#/tabelas?id=tabela-3-formas-de-pagamento">Tabela Auxiliar 3 - Formas de Pagamento</a>

Durante os testes em Sandbox, as compras que forem processadas com cartões de crédito poderão ser aprovadas ou reprovadas em tempo real. Este procedimento poderá ser realizado de acordo com o parcelamento escolhido:

**Aprovada**: transações com parcelamento ímpar (1, 3, 5, 7, 9, 11);

**Reprovada**: transações com parcelamento par (2, 4, 6, 8, 10, 12).


> Valor mínimo de transação de cartão de crédito é R$ 1,00


Altere o 'nó payment' para:

```javascript
	    "payment":{  
	       "payment_method_id":"3",
	       "card_name": "STEPHEN STRANGE",
	       "card_number": "4111111111111111",
	       "card_expdate_month": "01",
	       "card_expdate_year": "2021",
	       "card_cvv": "644",
	       "split": "1"
	    }
```


## Enviando uma transação

Para esta integração, deverá ser feito <span class="post">POST</span> uso da API a seguir:

| Endereço para Integração |                                                                              |
|--------------------------|----------------------------------------------------------------------------|
| Ambiente de Testes       | https://api.intermediador.sandbox.yapay.com.br/api/v3/transactions/payment |
| Ambiente de Produção     | https://api.intermediador.yapay.com.br/api/v3/transactions/payment |
| Protocolo                | Rest/HTTP                                                                  |

> É necessario utilizar o Protocolo de Criptografia TLS na versão 1.2. 

Abaixo você consegue visualizar um exemplo em cURL da criação de uma Transação em Cartão de Crédito:

> **Exemplo de criação de Transação com Cartão de Crédito**

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
                "payment_method_id":"3",
                "card_name":"STEPHEN STRANGE",
                "card_number":"4111111111111111",
                "card_expdate_month":"01",
                "card_expdate_year":"2021",
                "card_cvv":"644",
                "split":"1"
              }
            }'

```


> Resposta da API

A API de Transações retorna a resposta em <span class="post">JSON</span>.

Exemplo de resposta com sucesso, se baseando no envio do exemplo acima:


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
                "price_payment": "147.69",
                "price_original": "142.0",
                "payment_response": "Autorização aprovada",
                "url_payment": "",
                "tid": "10347871500026BF1001",
                "split": 3,
                "payment_method_id": 3,
                "payment_method_name": "Visa",
                "linha_digitavel": null
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

