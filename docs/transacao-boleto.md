# Boleto

Também é dispobilizada a funcionalidade de pagamentos com o meio de pagamento Boleto pela API de Transação. É de extrema importância a utilização do nosso fingerprint, abaixo você verá uma explicação mais detalhada sobre isso.

Basta você alterar o nó payment para:

```javascript
	    "payment":{  
	       "payment_method_id":"6"
	    }
```	    


## Código de Exemplo

Abaixo você consegue visualizar um exemplo em JSON da criação de uma Transação em Boleto:


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
	    "payment":{  
	       "payment_method_id":"6"
	    }
    }

```


