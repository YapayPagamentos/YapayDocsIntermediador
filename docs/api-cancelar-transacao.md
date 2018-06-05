# API Cancelar Transação 

<span class="patch">PATCH</span><span class="beforePost">/api/v3/transactions/cancel</span>


O Yapay disponibiliza uma versão transparente para cancelamento de transações, permitindo que seja cancelada a transação de forma transparente. 

Através do access_token e o id da transação, é possivel realizar um <span class="patch">PATCH</span> na API de Cancelamento de Transação. Lembrando que o access_token você pega utilizando a API de Autorização.


| Endereço para Integração                                                                          |
|--------------------------|------------------------------------------------------------------------|
| Ambiente de Testes       | https://api.intermediador.sandbox.yapay.com.br/api/v3/transactions/cancel   |
| Ambiente de Produção     | http://api.intermediador.yapay.com.br/api/v3/transactions/cancel           |
| Protocolo                | Rest                                                              |




# Códigos de Exemplo


```javascript
  {  
     "access_token":"SEU_ACCESS_TOKEN",
     "transaction_id": 20867,
     "reason_cancellation_id": "6"
  }
```


# Tabela de Campos

Para a integração via <span class="patch">PATCH</span>, segue abaixo os dados necessários para envio:


| Dados de Entrada                       |  Obrig.  | Descrição                                  |
|----------------------------------------|----------|--------------------------------------------|
| access_token                           |   Sim    |  Access Token de identificação do vendedor |
| transaction_id                         |   Sim    |  ID da Transação                           |
| reason_cancellation_id                 |   Sim    |  Motivo Cancelamento<sup>1</sup>           |


# Resposta da API

> Exemplo de resposta com `sucesso` baseando no envio do exemplo:

```javascript
    {
        "message_response": {
            "message": "success"
        },
        "data_response": {
            "transaction": {
                "order_number": "79717",
                "free": "Campo Livre",
                "transaction_id": 79717,
                "status_name": "Cancelada",
                "status_id": 7,
                "token_transaction": "4101779e6b84332c8a31dd730c00b0dc",
                "payment": {
                    "price_original": "142.0",
                    "price_payment": "142.0",
                    "payment_response": "",
                    "url_payment": "https://tc.intermediador.sandbox.yapay.com.br/payment/billet/774b33dd8d4a10809cb370b21d3bd",
                    "tid": null,
                    "split": 1,
                    "payment_method_id": 6,
                    "payment_method_name": "Boleto Bancario",
                    "linha_digitavel": "123123123123123131232131232131313211231321321"
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
                            "value": "11999999999",
                            "type_contact": "M"
                        },
                        {
                            "value": "4113096901",
                            "type_contact": "H"
                        }
                    ]
                }
            }
        }
    }
```


> Exemplo de resposta com `erro` baseando no envio do exemplo:

```javascript
{
    "message_response": {
        "message": "error"
    },
    "error_response": {
        "general_errors": [
            {
                "code": "003005",
                "message": "Transação inválida ou inexistente"
            }
        ]
    }
}
```



