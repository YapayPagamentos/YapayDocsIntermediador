# Realizando split de pagamento

Para que o repasse ao revendedor seja automático, utilizamos a API de Transação na integração com Marketplace informando os campos affiliates[], esses campos quando são enviados são identificamos que é referente a transações Marketplace:

| Dados de Entrada                      |  Obrig.  | Formato / Tam. Max   | Descrição                             |
|---------------------------------------|----------|----------------------|---------------------------------------|
|   affiliates[][account_email]         |   Não    | Texto / 100          | Email do afiliado da transação        |
|   affiliates[][percentage]            |   Não    | Número / 3           | Percentual de repasse ao afiliado     |
|   affiliates[][commission_amount]     |   Não    | Decimal / 11         | Valor de repasse ao afiliado          |


> Caso o afiliado não tenha cadastro na Yapay, o valor repassado fica aguardando o cadastro do afiliado.

# Código de Exemplo

Abaixo você consegue visualizar um exemplo em JSON da criação passando 15% para o afiliado `emaildoafiliado@afiliado.com`:


> **Exemplo em JSON**

```javascript
    {  
        "token_account":"SEU_TOKEN_AQUI",
        "customer":{  
            "contacts":[  
                {  
                    "type_contact":"H",
                    "number_contact":"1133221122"
                },{  
                    "type_contact":"M",
                    "number_contact":"11999999999"
                }         
            ],
            "addresses":[  
                {  
                    "type_address":"B",
                    "postal_code":"17000-000",
                    "street":"Av Themyscira",
                    "number":"1001",
                    "completion":"A",
                    "neighborhood":"Jd das Rochas",
                    "city":"Themyscira",
                    "state":"SP"
                }
            ],
            "name":"Diana Prince",
            "birth_date": "21/05/1941",
            "cpf":"50235335142",
            "email":"email@cliente.com.br"
        },
        "transaction_product":[  
            {  
                "description":"Camiseta Wonder Woman",
                "quantity":"1",
                "price_unit":"130.00",
                "code": "1",
                "sku_code": "0001",
                "extra": "Informação Extra"
            }
        ],
        "transaction":{  
            "available_payment_methods": "2,3,4,5,6,7,14,15,16,18,19,21,22,23",
            "customer_ip":"127.0.0.1",
            "shipping_type":"Sedex",
            "shipping_price":"12",
            "price_discount": "",
            "url_notification":"http://www.loja.com.br/notificacao",
            "free": "Campo Livre"      
            
        },

        "affiliates":[  
             {  
                 "account_email":"emaildoafiliado@afiliado.com",
                 "percentage":"15"
             }
         ],
         "payment":{  
            "payment_method_id":"3",
            "card_name": "DIANA PRINCE",
            "card_number": "4111111111111111",
            "card_expdate_month": "01",
            "card_expdate_year": "2021",
            "card_cvv": "644",
            "split": "1"
         }
    }

```


# Notificação Automática de Status

Para realizar a atualização automática do pedido, o Yapay pode realizar a comunicação a cada alteração de status de uma transação, fazendo com que seu sistema acompanhe todo o fluxo de status e esteja sempre atualizado quanto a situação da transação.

Dessa forma você precisa configurar uma URL que receberá a chamada, processará os dados recebidos, e em seguida irá obter mais detalhes da transação através da **API de Consulta de Transação**. Esse parâmetro está disponível em ambas as integrações (POST ou API) e chama-se `transaction[url_notification]`.