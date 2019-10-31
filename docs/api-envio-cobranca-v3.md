# API Envio de Cobrança v3

<span class="post">POST</span><span class="beforePost">/api/v3/charges</span>

A Yapay Intermediador fornece uma ferramenta poderosa para pessoas que desejam enviar um link com o envio de cobrança. Utilizando essa API o cliente receberá um e-mail com o valor para realizar o pagamento. 

Para utilizar a API Envio de Cobrança será necessário obter o token de acesso, utilizando a API de Autorização da Yapay. Você precisará informar parâmetros no `Header` para conseguir a autenticação.

Exemplo:

```
    Authorization: Token token=7cab2b1ca71a9d6cd26a46bt5e95b2be36ec165159a603054546d4fa58bce9p8, type=access_token
```



É possível enviar a quantidade de produtos editavel ou não.


| Endereço para Integração |                                                                               |
|--------------------------|-------------------------------------------------------------------------------|
| Ambiente de Testes       | https://api.intermediador.sandbox.yapay.com.br/api/v3/charges |
| Ambiente de Produção     | https://api.intermediador.yapay.com.br/api/v3/charges         |
| Protocolo                | Rest/HTTP                                                                     |

> É necessario utilizar o Protocolo de Criptografia TLS na versão 1.2. 

# Códigos de Exemplo


```javascript
{
	"order_number": "123456",
	"code": "12",
	"value": "12.50",
	"description": "Camiseta House Targaryen",
	"max_split_transaction": "2",
	"available_payment_methods": "6",
	"new_checkout": true,
	"use_cards": false,
	"customer_email": "emaildocliente@email.com"	
}
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
    "status": true,
    "created_at": 1572461048
}
```


> Exemplo de resposta com `erro` baseando no envio do exemplo:


```javascript
{
    "errors": [
        {
            "code": "038010",
            "message": "Número do pedido já existente"
        }
    ]
}
```



As mensagens de erros retornados pela API estão listadas na tabela abaixo:

| Código    |  Mensagem                                   |
|-----------|---------------------------------------------|
| 038010	  | Número do pedido já existente               |
| 038017    | Informe um número inteiro ou decimal separado por ponto (Exemplo: 15.75) |
| 038018    | É obrigatório informar a descrição          |



# Tabela de Parâmetros

Para a integração via <span class="post">POST</span>, segue abaixo os dados necessários para envio:

| Dados de Entrada                    |	Obrig.  |	Descrição                                            |
|-------------------------------------|---------|--------------------------------------------------------|
| access_token                        |	Sim     | Token de acesso                                        |
| customer_email                      | Não     | Envia solicitação para email informado                 |
| order_number                        | Sim     | Número do Pedido (não pode ser repetido)               |
| code                                | Não     | Código do Produto                                     |
| value                               | Sim     | Preço                                                  |
| description                         | Sim     | Descrição do produto                                   |
| max_split_transaction               | Não     | Valor máximo de parcela                                |
| available_payment_methods           | Não     | Formas de pagamento disponíveis para essa compra<sup>1</sup>. Enviando null aceitará todas [(Tabela)](https://intermediador.dev.yapay.com.br/#/tabelas?id=tabela-3-formas-de-pagamento) 
| new_checkout                        | Não     | Utilizará o novo checkout TRUE / FALSE |
| use_cards                           | Não     | Verifica cartões liberados para essa conta TRUE / FALSE |


> <sup>1</sup> Caso queira limitar as formas de pagamento, o parâmetro `use_cards` deve ser FALSE. 
