# API Cancelar Transação 

<span class="patch">PATCH</span><span class="beforePost">/api/v3/transactions/cancel</span>


A Yapay disponibiliza uma versão transparente para cancelamento de transações, permitindo que seja cancelada a transação de forma transparente. 

Através do `access_token` e o id da transação, é possivel realizar um <span class="patch">PATCH</span> na API de Cancelamento de Transação. Lembrando que o `access_token` você pega utilizando a [API de Autorização]()<sup>2<sup>.


| Endereço para Integração |                                                                         |
|--------------------------|------------------------------------------------------------------------|
| Ambiente de Testes       | https://api.intermediador.sandbox.yapay.com.br/api/v3/transactions/cancel   |
| Ambiente de Produção     | https://api.intermediador.yapay.com.br/api/v3/transactions/cancel           |
| Protocolo                | Rest                                                              |

> É necessario utilizar o Protocolo de Criptografia TLS na versão 1.2. 


# Códigos de Exemplo

Abaixo você consegue visualizar um exemplo do <span class="patch">PATCH</span> em cURL da criação de uma Transação em Cartão de Crédito:

```bash
    curl --request PATCH \
         --url 'https://api.intermediador.sandbox.yapay.com.br/api/v3/transactions/cancel' \
         --header 'Content-Type: application/json' \
         --data '  {  
                 "access_token":"SEU_ACCESS_TOKEN",
                 "transaction_id": 79717,
                 "reason_cancellation_id": "6"
                }'
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
                "order_number": "79717",
                "free": "Campo Livre",
                "transaction_id": 79717,
                "status_name": "Cancelada",
                "status_id": 7,
                "token_transaction": "4101779e6b84332c8a31pd730c00b0dc",
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
                    "name": "Stephen Strange",
                    "cpf": "37573138792",
                    "email": "stephen.strange@avengers.com",
                    "company_name": "",
                    "trade_name": "",
                    "cnpj": "",
                    "addresses": [
                        {
                            "street": "Av Esmeralda",
                            "number": "1001",
                            "neighborhood": "Jd Esmeralda",
                            "postal_code": "17000000",
                            "completion": "A",
                            "city": "Marilia",
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



# Tabela de Campos

Para a integração via <span class="patch">PATCH</span>, segue abaixo os dados necessários para envio:


| Dados de Entrada                       |  Obrig.  | Descrição                                  |
|----------------------------------------|----------|--------------------------------------------|
| access_token                           |   Sim    |  Access Token de identificação do vendedor |
| transaction_id                         |   Sim    |  ID da Transação                           |
| reason_cancellation_id                 |   Sim    |  Motivo Cancelamento<sup>1</sup>           |


> <sup>1</sup> Essa opção é necessário informar o motivo `6`. O Motivo 6 é relacionado ao **CANCELAMENTO PELA LOJA**, as outras opções são relacionadas ao cancelamento feito pelo cliente.

> <sup>2</sup> Para maiores informações sobre esta API, entre em contato com através do email **integracao@yapay.com.br**.
