# Consulta da Transação

Após receber esta informação, você pode consultar as informações completas da transação através da **API de Consulta de Transação**.

<span class="get">GET</span><span class="beforePost">/api/v3/transactions/get_by_token</span>


# Códigos de Exemplo


```bash
    curl --request GET \
         --url 'https://api.intermediador.sandbox.yapay.com.br/api/v3/transactions/get_by_token?token_account=SEU_TOKEN&token_transaction=cb22c716c80ddbaa16f8b8dbc49302a2' \
         --data '{}'
```



# Resposta da API

> Exemplo de resposta com `sucesso` baseando no envio do exemplo:

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
                "price_original": "142.0",
                "price_payment": "147.69",
                "payment_response": "Autorização aprovada",
                "url_payment": "",
                "tid": "10347871500026BF1001",
                "split": 3,
                "payment_method_id": 4,
                "payment_method_name": "Mastercard",
                "linha_digitavel": null
            },
            "customer": {
                "name": "Diana Prince",
                "cpf": "37573138792",
                "email": "dianaprince9834347522@amaf4343sdfdsfdszonas1587.com",
                "company_name": "",
                "trade_name": "",
                "cnpj": "",
                "addresses": [
                    {
                        "street": "Av Themyscira",
                        "number": "1001",
                        "neighborhood": "Jd das Rochas",
                        "postal_code": "17000000",
                        "completion": "A",
                        "city": "Themyscira",
                        "state": "SP"
                    }
                ],
                "contacts": [
                    {
                        "value": "1133221122",
                        "type_contact": "H"
                    },
                    {
                        "value": "11999999999",
                        "type_contact": "M"
                    }
                ]
            }
        }
    }
}

```

