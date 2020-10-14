# API de Código de Rastreio




<span class="post">POST</span><span class="beforePost">/v1/transactions/trace</span>


A Yapay disponibiliza uma versão transparente para a integração do código de postagem do produto da transação.

| Endereço para Integração |                                                                           |
|--------------------------|---------------------------------------------------------------------------|
| Ambiente de Testes       | https://api.intermediador.sandbox.yapay.com.br/api/v1/transactions/trace  |
| Ambiente de Produção     | https://api.intermediador.yapay.com.br/api/v1/transactions/trace          |
| Protocolo                | Rest/HTTP                                                                 |

> É necessario utilizar o Protocolo de Criptografia TLS na versão 1.2. 

**Dica: Sempre que a forma de entrega for CORREIOS deve ser enviado no parâmetro `url` a URL do Correios: `http://www2.correios.com.br/sistemas/rastreamento/`**

# Códigos de Exemplo


```javascript
    {
      "access_token": "ACCESS_TOKEN DO VENDEDOR",
      "order_number": "109948440",
      "url": "www.teste.com.br",
      "code": "AB84848484884BR",
      "tag_search": "",
      "date_posting": "07/06/2018",
      "date_estimed": "12/06/2018",
      "type_response": "J"
    }
```


# Resposta da API

> Exemplo de resposta em JSON com `sucesso` baseando no envio do exemplo:

```javascript
    {
        "message_response": {
            "message": "success"
        },
        "data_response": {
            "transaction_traces": [
                {
                    "transaction_trace": {
                        "id": 255,
                        "transaction_id": 109440,
                        "url": "www.teste.com.br",
                        "code": "AB84848484884BR",
                        "date_posting": "2018-06-07",
                        "date_estimed": "2018-06-12",
                        "date_confirmated": null,
                        "tag_search": "",
                        "created_at": "2018-06-07T18:07:58.000-03:00",
                        "updated_at": "2018-06-07T18:07:58.000-03:00"
                    }
                }
            ]
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


As mensagens de erros retornados pela API estão listadas na tabela abaixo:

| Código    |  Mensagem                                        |
|-----------|--------------------------------------------------|
| 003006    | Pedido inválido                                  |
| 017001    | Token de sessão inválido                         |
| 060003    | Token de acesso inválido ou expirado.            |


# Tabela de Parâmetros

Para a integração via <span class="post">POST</span>, segue abaixo os dados necessários para envio:

| Dados de Entrada  |  Obrig.  | Descrição                                |
|-------------------|----------|------------------------------------------|
| access_token      | Sim      | Token de acesso                          |
| order_number      | Sim      | Número do pedido                         |
| url               | Não      | URL do site de consulta de postagem      |
| code              | Sim      | Código de postagem                       |
| tag_search        | Não      | Tag de Busca                             |
| date_posting      | Sim      | Data de Postagem                         |
| date_estimed      | Não      | Data estimada de entrega                 |
| type_response     | Não      | Tipo de Resposta J = JSON | Outros = XML |
