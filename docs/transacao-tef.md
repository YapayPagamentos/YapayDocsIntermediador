# Transferência Bancária

Também é dispobilizada a funcionalidade de pagamentos com o meio de pagamento por Transferência Bancária pela API de Transação. É de extrema importância a utilização do nosso fingerprint, abaixo você verá uma explicação mais detalhada sobre isso.

Você pode visualizar os IDs para as formas de pagamento na nossa <a href="/#/tabelas?id=tabela-3-formas-de-pagamento">Tabela Auxiliar 3 - Formas de Pagamento</a>

Basta você alterar o nó payment para:

```javascript
	    "payment":{  
	       "payment_method_id":"7"
	    }
```	    


## Enviando uma transação


Para esta integração, deverá ser feito <span class="post">POST</span> uso da API a seguir:

| Endereço para Integração |                                                                            |
|--------------------------|----------------------------------------------------------------------------|
| Ambiente de Testes       | https://api.intermediador.sandbox.yapay.com.br/api/v3/transactions/payment |
| Ambiente de Produção     | https://api.intermediador.yapay.com.br/api/v3/transactions/payment |
| Protocolo                | Rest/HTTP                                                                  |

> É necessario utilizar o Protocolo de Criptografia TLS na versão 1.2. 

Abaixo você consegue visualizar um exemplo em cURL da criação de uma Transação em Transferência Bancária pelo Ítau:


> **Exemplo de criação de Transação com Transferência Bancária para Ítau**

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
                "payment_method_id":"7"
              }
            }'

```



> Resposta da API

A API de Transações retorna a resposta em JSON. Observe que no retorno você recebe dentro do nó payment o campo `url_payment`, com esse campo você pode fazer o redirecionamento para o cliente realizar o pagamento. Importante: Não pode ser `iframe`.

Exemplo de resposta com sucesso baseando no envio do exemplo acima:


```javascript
{
    "message_response": {
        "message": "success"
    },
    "data_response": {
        "transaction": {
            "order_number": "11384683",
            "free": "Campo Livre",
            "transaction_id": 11384683,
            "status_name": "Aguardando Pagamento",
            "status_id": 4,
            "token_transaction": "c4988bb7836b2a887d1d55b67bc97a27",
            "payment": {
                "price_payment": "142.0",
                "price_original": "142.0",
                "payment_response": "",
                "url_payment": "https://gtw.checkout.tray.com.br/api/print/1c2a5a9bf4c7a167dff6098b7afe704f",
                "tid": null,
                "split": 1,
                "payment_method_id": 7,
                "payment_method_name": "Transf. Online Itaú",
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




