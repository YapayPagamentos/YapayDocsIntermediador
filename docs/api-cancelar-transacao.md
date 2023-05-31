# API Cancelar Transação 

<span class="patch">PATCH</span><span class="beforePost">/api/v3/transactions/cancel</span>


A Vindi disponibiliza uma versão transparente para cancelamento de transações, permitindo que seja cancelada a transação de forma transparente. Esse cancelamento pode ser SÍNCRONO ou ASSÍNCRONO.

> O prazo para cancelamento via API é de 90 dias, após esse período é necessário entrar em contato com a Vindi.

Através do `access_token` e o id da transação, é possivel realizar um <span class="patch">PATCH</span> na API de Cancelamento de Transação. Lembrando que o `access_token` você pega utilizando a [API de Autorização]()<sup>1</sup>.


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
                 "transaction_id": 79717
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

# API Cancelar Transação com Estorno Parcial

A API de Cancelar Transação permite que seja realizado o estorno parcial da transação, para isso você deve enviar o parâmetro `refund_amount`. 



# Códigos de Exemplo

Abaixo você consegue visualizar um exemplo do <span class="patch">PATCH</span> em cURL da criação de uma Transação em Cartão de Crédito:

```bash
    curl --request PATCH \
         --url 'https://api.intermediador.sandbox.yapay.com.br/api/v3/transactions/cancel' \
         --header 'Content-Type: application/json' \
         --data '  {  
                 "access_token":"SEU_ACCESS_TOKEN",
                 "transaction_id": 79717,
                 "refund_amount": "10.0"
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
                "refunds": [
                    {
                        "id": 54861,
                        "value": 10.0,
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



# Tabela de Campos

Para a integração via <span class="patch">PATCH</span>, segue abaixo os dados necessários para envio:


| Dados de Entrada                       |  Obrig.  | Descrição                                  |
|----------------------------------------|----------|--------------------------------------------|
| access_token                           |   Sim    |  Access Token de identificação do vendedor |
| transaction_id                         |   Sim    |  ID da Transação                           |
| refund_amount                          |   Não    |  Valor do estorno parcial                  |
| message_cancellation                   |   Não    |  Mensagem de Cancelamento                  |



# Fluxo Síncrono e Assíncrono

## Síncrono

Esse fluxo será síncrono quando o recebível da transação que está sendo solicitado o cancelamento NÃO for creditado. Será retornado de imediato que o cancelamento da transação foi concluído.

## Assíncrono

No fluxo assíncrono, significa que o recebível da transação já foi creditado na conta bancária do cliente, ao solicitar o cancelamento será criada uma solicitação de cancelamento que ficará com o status Pendente até que a Vindi consiga realizar recuperar o valor informado. Ou seja, a transação continuará com o status 6-Aprovada. 

Importante SEMPRE realizar a consulta pelo endpoint <span class="patch">GET</span><span class="beforePost">/api/v3/transactions/get_by_token_brief</span> terá a informação no nó `refunds`, com os seguintes status:

| ID Status | Status de Cancelamento | Observação do Status |
|-----------|------------------------|----------------------|
| 155 | Pendente | Status significa que a solicitação de estorno está PENDENTE de recuperação do valor |
| 156 | Aguardando confirmação | Status significa a solicitação de estorno está aguardando confirmação da recuperação do valor |
| 157 | Finalizado | Status significa que a solicitação de estorno está FNIALIZADA, ou seja conseguimos recuperar o valor |
| 161 | Cancelado | Status significa que a solicitação de estorno foi Cancelada |
| 183 | Expirado | Status significa que a solicitação de estorno foi EXPIRADA, ou seja não conseguimos recuperar o valor para o cancelamento. Se o comprador ainda quiser o cancelamento será necessário solicitar novamente o cancelamento. |



```javascript
         "refunds":[
            {
               "id":26065839,
               "value":15.0,
               "observation":"Cancelamento",
               "status_id":155,
               "status_name":"Pendente",
               "refund_kind_id":53,
               "refund_kind_name":"refund_kind_full",
               "refund_method_id":55,
               "refund_method_name":"refund_method_balance",
               "created_at":1678714901
            }
         ],
```

# Estorno de Boleto/TEF novo fluxo Automatização de Reembolso


Com o novo fluxo de [Automatização de Reembolso](https://atendimento.yapay.com.br/hc/pt-br/articles/13144282149403-Automatiza%C3%A7%C3%A3o-de-estorno-e-reembolso-de-pagamentos), o cancelamento de transações Boleto e TEF deverão ser feitas, obrigatoriamente, com os dados da conta bancária do comprador.
# Códigos de Exemplo

Observe abaixo que na requisição de uma transação Boleto ou TEF, é adicionado o nó `bank_account[]` para inclusão dos dados bancários do comprador:

```bash
    curl --request PATCH \
         --url 'https://api.intermediador.sandbox.yapay.com.br/api/v3/transactions/cancel' \
         --header 'Content-Type: application/json' \
         --data '  {  
                 "access_token":"SEU_ACCESS_TOKEN",
                 "transaction_id": 79717,
                 "bank_account": {
                      "agency_number": "0011",
                      "account_number": "12345",
                      "account_digit": "6",
                      "account_type": "C",
                      "bank_code": "33"
                      }                 
                }'
```
