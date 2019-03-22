# API Consultar Transação

<span class="get">GET</span><span class="beforePost">/api/v3/transactions/get_by_token</span>

O Yapay disponibiliza um recurso para a consulta da transação. Com este recurso, você poderá realizar a consulta para obter as informações detalhadas da transação, e assim comparar as informações e atualizar o status do pedido com segurança.

Para esta integração, deverá ser feito uso da API a seguir:

| Endereço para Integração |                                                                                  |
|--------------------------|---------------------------------------------------------------------------------|
| Ambiente de Testes       | https://api.intermediador.sandbox.yapay.com.br/api/v3/transactions/get_by_token |
| Ambiente de Produção     | https://api.intermediador.yapay.com.br/v3/transactions/get_by_token              |
| Protocolo                | Rest/HTTP                                                                       |

> É necessario utilizar o Protocolo de Criptografia TLS na versão 1.2. 

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
            "token_transaction": "cb22c716c80ddpaa16f8b8dbc49302a2",
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


> Exemplo de resposta com `erro` baseando no envio do exemplo:


```javascript
{
    "message_response": {
        "message": "error"
    },
    "error_response": {
        "general_errors": [
            {
                "code": "001001",
                "message": "Token inválido ou não encontrado"
            }
        ]
    }
}
```


# Tabela de Parâmetros

Para a integração via <span class="get">GET</span>, segue abaixo os dados necessários para envio:

| Dados de Entrada                       |  Obrig.  | Formato   | Descrição                                                |
|----------------------------------------|----------|-----------|----------------------------------------------------------|
| token_account                          | Sim      |  Texto    |  Token de identificação do vendedor                      |         
| token_transaction                      | Sim      |  Texto    |  Token de identificação da transação                     |


