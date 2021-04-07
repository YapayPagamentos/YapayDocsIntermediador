# API Consultar Transação

<span class="get">GET</span><span class="beforePost">/api/v3/transactions/get_by_token_brief</span>

O Yapay disponibiliza um recurso para a consulta da transação. Com este recurso, você poderá realizar a consulta para obter as informações detalhadas da transação, e assim comparar as informações e atualizar o status do pedido com segurança.

> Para adequação da Lei Geral de Proteção de Dados - LGPD, a API de Consulta de Transação não retorna os dados do cliente da compra.


Para esta integração, deverá ser feito uso da API a seguir:

| Endereço para Integração |                                                                                  |
|--------------------------|---------------------------------------------------------------------------------|
| Ambiente de Testes       | https://api.intermediador.sandbox.yapay.com.br/api/v3/transactions/get_by_token_brief |
| Ambiente de Produção     | https://api.intermediador.yapay.com.br/api/v3/transactions/get_by_token_brief              |
| Protocolo                | Rest/HTTP                                                                       |

> É necessario utilizar o Protocolo de Criptografia TLS na versão 1.2. 

# Códigos de Exemplo


```bash
    curl --request GET \
         --url 'https://api.intermediador.sandbox.yapay.com.br/api/v3/transactions/get_by_token_brief?token_account=SEU_TOKEN&token_transaction=2c40fb33783f418ce1f0848515dcb3d4' \
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
            "order_number": "613620",            
            "transaction_id": 613620,
            "status_name": "Cancelada",
            "status_id": 7,
            "token_transaction": "2c40fb33783f418ce1f0848515dcb3d4",
            "payment": {
                "price_original": "650.0",
                "price_payment": "650.0",
                "payment_response": null,
                "url_payment": "https://intermediador-sandbox.yapay.com.br/orders/billet/2c40fb33783f418ce1f0848515dcb3d4",
                "tid": "00000642891",
                "split": 1,
                "payment_method_id": 6,
                "payment_method_name": "Boleto Bancario",
                "linha_digitavel": "23790.00124  60000.064281  91123.456708  7  88310000065000",
                "date_payment": 1617591600,
                "date_approval": 1617591600
            },
            "refunds": [
                {
                    "id": 281572,
                    "value": 650.0,
                    "observation": "Cancelamento",
                    "status_id": 157,
                    "status_name": "Finalizado",
                    "refund_kind_id": 53,
                    "refund_kind_name": "refund_kind_full",
                    "refund_method_id": 54,
                    "refund_method_name": "refund_method_withdraw",
                    "created_at": 1617634787
                }
            ]
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


