# API Listagem de Transações

<span class="get">GET</span><span class="beforePost">/api/v3/sales</span>

A Yapay disponibiliza um recurso para a listagem de transações. Com este recurso, você poderá realizar a listagem para obter as informações detalhadas das transações, e assim comparar as informações e atualizar o status do pedido com segurança.

Para utilizar a API Listagem de Transações será necessário obter o token de acesso, utilizando a [API de Autorização]() <sup>1<sup>
da Yapay. Você precisará informar parâmetros no `Header` para conseguir a autenticação.

Exemplo:

```
    Authorization: Token token=SEU_ACCESS_TOKEN, type=access_token
```


Para esta integração, deverá ser feito uso da API a seguir:

| Endereço para Integração |                                                             |
|--------------------------|-------------------------------------------------------------|
| Ambiente de Testes       | https://api.intermediador.sandbox.yapay.com.br/api/v3/sales |
| Ambiente de Produção     | https://api.intermediador.yapay.com.br/api/v3/sales         |
| Protocolo                | Rest/HTTP                                                                |

> É necessario utilizar o Protocolo de Criptografia TLS na versão 1.2. 

> <sup>1</sup> Para maiores informações sobre esta API, entre em contato com através do email **integracao@yapay.com.br**.

# Códigos de Exemplo

Criando <span class="get">GET</span> de listagem de todas as transações:

```bash
    curl --request GET \
         --url 'https://api.intermediador.sandbox.yapay.com.br/api/v3/sales' \
         --header 'Authorization: Token token=p07511206953c5e62dccfa320k74a17fc9838ac287765641a8e65ab32740ddb0, type=access_token' \
         --data '{}'
```


Criando <span class="get">GET</span> de uma transação especifica:

```bash
    curl --request GET \
         --url 'https://api.intermediador.sandbox.yapay.com.br/api/v3/sales?id=109657' \
         --header 'Authorization: Token token=p07511206953c5e62dccfa320k74a17fc9838ac287765641a8e65ab32740ddb0, type=access_token' \
         --data '{}'
```


# Resposta da API

> Exemplo de resposta com `sucesso` baseando no envio do exemplo:

```javascript
    {
        "resource": "list",
        "pagination": {
            "current_page": 0,
            "per_page": 20,
            "page_amount": 1,
            "count": 1
        },
        "data": [
            {
                "resource": "sale",
                "id": 109661,
                "order_number": "109661",
                "original_price": 142,
                "tax": 9.469999999999999,
                "seller_price": 132.53,
                "payment_price": 142,
                "discount_price": 0,
                "sub_store": "",
                "created": 1528469296,
                "updated": 1528469296,
                "schedulings": {
                    "resource": "list",
                    "data": [],
                    "options": {
                        "total_amount": 0,
                        "all_status": [
                            [
                                "to_credit",
                                12
                            ],
                            [
                                "blocked_down_payment",
                                13
                            ],
                            [
                                "blocked_canceled",
                                14
                            ],
                            [
                                "finalized",
                                15
                            ],
                            [
                                "processed_early",
                                16
                            ]
                        ]
                    }
                },
                "remaining_time_to_open_dispute": null,
                "status": {
                    "resource": "status",
                    "name": "waiting_payment",
                    "id": 4
                },
                "url_notification": "",
                "payment": {
                    "resource": "payment",
                    "tid": null,
                    "payment_method_id": 6,
                    "payment_method_name": "Boleto Bancario",
                    "installments": 1,
                    "payment_url": "https://tc.intermediador.sandbox.yapay.com.br/payment/billet/2536492c4170741fc15e146ea82cadb9",
                    "typeful_line": "123123123123123131232131232131313211231321321"
                },
                "customer": {
                    "resource": "customer",
                    "name": "Stephen Strange",
                    "email": "stephen.strange@avengers.com",
                    "cpf": "37573138792",
                    "phone": "1433225544"
                },
                "seller": {
                    "resource": "seller",
                    "name": "Thanos Titã",
                    "email": "thanos@tita.com",
                    "cpf": "34236440440",
                    "cnpj": null,
                    "phone": "1433225544"
                },
                "transaction_products": [
                    {
                        "resource": "transaction_product",
                        "code": "1",
                        "description": "Infinity Stone",
                        "extra": "",
                        "unit_price": 130,
                        "quantity": "1.0",
                        "sku_code": "0001",
                        "img_url": null
                    }
                ],
                "shipping": {
                    "resource": "shipping",
                    "shipping_price": 12,
                    "shipping_type": "Sedex",
                    "tracking_code": null,
                    "tracking_url": null,
                    "posted_date": null,
                    "address": {
                        "resource": "address",
                        "id": 138681,
                        "active": true,
                        "primary": true,
                        "postal_code": "17000000",
                        "street": "Av Themyscira",
                        "complement": "A",
                        "number": "1001",
                        "neighborhood": "Jd das Rochas",
                        "city": "Themyscira",
                        "state": "SP",
                        "type": "billing"
                    }
                }
            }
        ],
        "options": {
            "sum_price_original": 142,
            "sum_tax": 9.469999999999999,
            "sum_price_seller": 132.53,
            "sum_price_payment": 142,
            "columns": {}
        }
    }

```

> Nessa API o nó status[name] é retornado em inglês. Veja em <a href="/#/tabelas?a=22&id=tabela-4-status-da-transa%c3%a7%c3%a3o">Tabela 4 - Status da Transação</a> 


# Tabela de Parâmetros

Para a integração via <span class="get">GET</span>, segue abaixo os dados necessários para envio:

| Dados de Entrada  | Obrig. | Descrição                                 |
|-------------------|--------|-------------------------------------------|
| token             | Sim    | Token de Acesso ou Session ID             |         
| type              | Sim    | Tipo de acesso access_token ou session_id |
| id                | Não    | ID da Transação                           |
