# API Cancelar Transação com Split

<span class="patch">PATCH</span><span class="beforePost">/api/v3/transactions/cancel</span>


A Vindi Pagamentos disponibiliza uma versão transparente de cancelamento das transações com split via API.

> O prazo para cancelamento via API é de 90 dias, após esse período é necessário entrar em contato com a Vindi Pagamentos.

Através do `access_token` e o id da transação, é possivel realizar um <span class="patch">PATCH</span> na API de Cancelamento de Transação. Lembrando que o `access_token` você pega utilizando a [API de Autorização]()<sup>1</sup>.


| Endereço para Integração |                                                                         |
|--------------------------|------------------------------------------------------------------------|
| Ambiente de Testes       | https://api.intermediador.sandbox.yapay.com.br/api/v3/transactions/cancel   |
| Ambiente de Produção     | https://api.intermediador.yapay.com.br/api/v3/transactions/cancel           |
| Protocolo                | Rest                                                              |

> É necessario utilizar o Protocolo de Criptografia TLS na versão 1.2. 


# Códigos de Exemplo

Abaixo você consegue visualizar um exemplo do <span class="patch">PATCH</span> em cURL da criação de uma Transação em Cartão de Crédito:

> Em caso de transações com afiliados, **sempre** deve ser informado os valores do estorno da transação e o valor do estorno do afiliado.

```bash
    curl --request PATCH \
         --url 'https://api.intermediador.sandbox.yapay.com.br/api/v3/transactions/cancel' \
         --header 'Content-Type: application/json' \
         --data '  {  
                 "access_token":"SEU_ACCESS_TOKEN",
                 "transaction_id": 79717,             
                  "refund_amount": "1000",
                "split_refunds": [
                   {
                       "account_email": "wanda.maximoff@avengers.com",
                       "refund_amount": "100",
                       "message_cancellation": "Cliente não quer mais o produto"
                   }
                 ]
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
                    "price_original": "1000.0",
                    "price_payment": "1000.0",
                    "payment_response": "",
                    "url_payment": "https://tc.intermediador.sandbox.yapay.com.br/payment/billet/774b33dd8d4a10809cb370b21d3bd",
                    "tid": null,
                    "split": 1,
                    "payment_method_id": 6,
                    "payment_method_name": "Boleto Bancario",
                    "linha_digitavel": "123123123123123131232131232131313211231321321"
                },
                "refunds": [
                    {
                        "id": 54860,
                        "value": 1000.0,
                        "observation": "Cancelamento",
                        "status_id": 157,
                        "status_name": "Finalizado",
                        "refund_kind_id": 52,
                        "refund_kind_name": "refund_kind_partial",
                        "refund_method_id": 55,
                        "refund_method_name": "refund_method_balance",
                        "created_at": 1582218221
                    }
                ],                     
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

# API Cancelar Transação com Estorno Parcial com Split

A API de Cancelar Transação permite que seja realizado o estorno parcial da transação, para isso você deve enviar o parâmetro `refund_amount`. 



# Códigos de Exemplo

Abaixo você consegue visualizar um exemplo do <span class="patch">PATCH</span> em cURL da criação de uma Transação em Cartão de Crédito:

> Em caso de transações com afiliados, **sempre** deve ser informado os valores do estorno da transação e o valor do estorno do afiliado.


```bash
    curl --request PATCH \
         --url 'https://api.intermediador.sandbox.yapay.com.br/api/v3/transactions/cancel' \
         --header 'Content-Type: application/json' \
         --data '  {  
                 "access_token":"SEU_ACCESS_TOKEN",
                 "transaction_id": 79717,
                 "refund_amount": "500",
                "split_refunds": [
                   {
                       "account_email": "wanda.maximoff@avengers.com",
                       "refund_amount": "50",
                       "message_cancellation": "Cliente não quer um dos produtos"
                   }
                 ]                 
                }'
```



# Resposta da API

> Exemplo de resposta com `sucesso` baseando no envio do exemplo, observe que será retornado o nó `refunds`:

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
                    "price_original": "1000.0",
                    "price_payment": "1000.0",
                    "payment_response": "",
                    "url_payment": "https://tc.intermediador.sandbox.yapay.com.br/payment/billet/774b33dd8d4a10809cb370b21d3bd",
                    "tid": null,
                    "split": 1,
                    "payment_method_id": 6,
                    "payment_method_name": "Boleto Bancario",
                    "linha_digitavel": "123123123123123131232131232131313211231321321"
                },
                "refunds": [
                    {
                        "id": 54861,
                        "value": 500.0,
                        "observation": "Cancelamento",
                        "status_id": 157,
                        "status_name": "Finalizado",
                        "refund_kind_id": 52,
                        "refund_kind_name": "refund_kind_partial",
                        "refund_method_id": 55,
                        "refund_method_name": "refund_method_balance",
                        "created_at": 1582218221
                    }
                ],        
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
                "code": "105012",
                "message": "Para realizar um estorno parcial é necessário que o processamento esteja aprovado"
            }
        ]
    }
}
```

As mensagens de erros retornados pela API estão listadas na tabela abaixo:

| Código    |  Mensagem                                        | Solução                                               |
|-----------|--------------------------------------------------|-------------------------------------------------------|
|  000000   |     Invalid Message! Email do afiliado informado não pertence a esse pedido             | Verificar se o `account_email` é referente ao afiliado da transação                            |
|  003005   |     Transação inválida             | Transação não pertence a esse vendedor                            |
|  999002   |     Ação não permitida             | Autenticação inválida / Parâmetros com nomes incorretos                            |
|  105012   |     Para realizar um estorno parcial é necessário que o processamento esteja aprovado             | Transação com estorno parcial deve estar com status Aprovado                            |



# Tabela de Campos

Para a integração via <span class="patch">PATCH</span>, segue abaixo os dados necessários para envio:


| Dados de Entrada                       |  Obrig.  | Descrição                                  |
|----------------------------------------|----------|--------------------------------------------|
| access_token                           |   Sim    |  Access Token de identificação do vendedor |
| transaction_id                         |   Sim    |  ID da Transação                           |
| refund_amount                          |   Não    |  Valor do estorno parcial                  |
| message_cancellation                   |   Não    |  Mensagem de Cancelamento                  |
| split_refunds[account_email]           |   Sim    |  Email do afiliado                         |
| split_refunds[refund_amount]           |   Sim    |  Valor a ser estornado do Afiliado                                               |
| split_refunds[message_cancellation]    |   Sim    |  Mensagem de cancelamento (Aparecerá para no portal do Afiliado)                  |



> <sup>1</sup> Para maiores informações sobre esta API, entre em contato com através do email **integracao@yapay.com.br**.
