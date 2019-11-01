# API Inativar Cobrança v3

<span class="post">POST</span><span class="beforePost">/api/v3/charges</span>

Para inativar uma cobrança, é possível utilizando a API de Inativar Cobrança

Para utilizar a API Envio de Cobrança será necessário obter o token de acesso, utilizando a API de Autorização da Yapay. Você precisará informar parâmetros no `Header` para conseguir a autenticação.

Exemplo:

```
    Authorization: Token token=7cab2b1ca71a9d6cd26a46bt5e95b2be36ec165159a603054546d4fa58bce9p8, type=access_token
```


É possível enviar a quantidade de produtos editavel ou não.


| Endereço para Integração |                                                                               |
|--------------------------|-------------------------------------------------------------------------------|
| Ambiente de Testes       | https://api.intermediador.sandbox.yapay.com.br/api/v3/charges/:id/inactivate |
| Ambiente de Produção     | https://api.intermediador.yapay.com.br/api/v3/charges/:id/inactivate         |
| Protocolo                | Rest/HTTP                                                                     |

> É necessario utilizar o Protocolo de Criptografia TLS na versão 1.2. 

# Códigos de Exemplo


```bash
    curl --request POST \
         --url 'https://api.intermediador.sandbox.yapay.com.br/api/v3/charges/974/inactivate' \
         --header 'Authorization: Token token=p07511206953c5e62dccfa320k74a17fc9838ac287765641a8e65ab32740ddb0, type=access_token' \
         --data '{}'
```


# Resposta da API

> Exemplo de resposta em JSON com `sucesso` baseando no envio do exemplo:

```javascript
{
    "resource": "charge",
    "id": 974,
    "order_number": "123456",
    "code": "12",
    "value": "12.5",
    "description": "Camiseta House Targaryen",
    "max_split_transaction": 2,
    "available_payment_methods": "6",
    "payment_link": "https://pagar.online/b7tg",
    "status": false,
    "created_at": 1572461048
}
```


> Exemplo de resposta com `erro` baseando no envio do exemplo:


```javascript
{
    "errors": [
        {
            "code": "050001",
            "message": "Cobrança não encontrada"
        }
    ]
}
```



As mensagens de erros retornados pela API estão listadas na tabela abaixo:

| Código    |  Mensagem               |
|-----------|-------------------------|
| 050001	  | Cobrança não encontrada |




# Tabela de Parâmetros

Para a integração via <span class="post">POST</span>, segue abaixo os dados necessários para envio:

| Dados de Entrada  |	Obrig.  |	Descrição      |
|----------------- -|---------|----------------|
| id                |	Sim     | ID da Cobrança |



