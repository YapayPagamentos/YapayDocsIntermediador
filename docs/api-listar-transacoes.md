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
            "id": 364815,
            "order_number": "364815",
            "original_price": 142.0,
            "tax": 3.0900000000000034,
            "seller_price": 138.91,
            "payment_price": 142.0,
            "discount_price": 0.0,
            "additional_price": 0.0,
            "sub_store": "",
            "created": 1583514061,
            "updated": 1583514070,
            "schedulings": {
                "resource": "list",
                "data": []
            },
            "remaining_time_to_open_dispute": null,
            "status": {
                "resource": "status",
                "name": "waiting_payment",
                "id": 4
            },
            "status_changed_at": 1583514061,
            "url_notification": "https://urlnotificacao.com/1ehx4741",
            "transaction_token": "8da3123373bb1e9fc32de71b9ca3b16",
            "contestation_id": null,
            "canceled_by": "",
            "fraud_confirmated": false,
            "payment": {
                "resource": "payment",
                "tid": "",
                "payment_method_id": 3,
                "payment_method_name": "Visa",
                "installments": 1,
                "payment_url": null,
                "typeful_line": null
            },
            "customer": {
                "resource": "customer",
                "name": "Stephen Strange",
                "business_name": null,
                "email": "stephen.strange@avengers.com",
                "cpf": "50235335142",
                "cnpj": null,
                "phone": "1133221122"
            },
            "seller": {
                "resource": "seller",
                "name": "Tony Stark Store",
                "email": "tony@stark.com",
                "cpf": "37558792045",
                "cnpj": null,
                "phone": "1499999999"
            },
            "transaction_products": [
                {
                    "resource": "transaction_product",
                    "code": "1",
                    "description": "Camiseta Tony Stark",
                    "extra": "Informação Extra",
                    "unit_price": 130.0,
                    "quantity": "1.0",
                    "sku_code": "0001",
                    "img_url": null
                }
            ],
            "shipping": {
                "resource": "shipping",
                "shipping_price": 12.0,
                "shipping_type": "Sedex",
                "tracking_code": null,
                "tracking_url": null,
                "posted_date": null,
                "address": {
                    "resource": "address",
                    "id": 152154,
                    "active": true,
                    "primary": false,
                    "postal_code": "17000000",
                    "street": "Rua Bleecker",
                    "complement": "A",
                    "number": "177",
                    "neighborhood": "Greenwich Village",
                    "city": "Nova York",
                    "state": "SP",
                    "type": "billing"
                }
            }
        }
    ],
    "options": {
        "sum_price_original": 142.0,
        "sum_tax": 3.0900000000000034,
        "sum_price_seller": 138.91,
        "sum_price_payment": 142.0,
        "columns": {
            "buyer_seller": "true",
            "tracking": "true",
            "payment_method": "true",
            "tax": "false",
            "price_seller": "false",
            "price_payment": "false"
        }
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
| status            | Não    | Status                                    |
| id                | Não    | ID da Transação                           |
| order_number      | Não    | Número do Pedido                          |
| customer          | Não    | Cliente (email ou Nome)                   |
| start_date_created | Não   | Data inicial de Criação                   |
| end_date_created  | Não    | Data final de Criação                     |
| current_page      | Não    | Página                                    |
| per_page          | Não    | Transações por página                     |


