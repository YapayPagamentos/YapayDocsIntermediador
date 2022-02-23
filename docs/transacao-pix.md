## PIX


A forma de pagamento **PIX** na Yapay já está disponível para todos na criação de transações pela API de Transação.

Para utilizar é simples, você precisa passar o `payment_method_id` igual a `27`. No response da API vem os seguintes campos:

| Campo                | Descrição campo                                                            |
|----------------------|----------------------------------------------------------------------------|
| url_payment          | URL de Pagamento para direcionar o cliente para pagamento                  |
| qrcode_path          | URL da imagem SVG do QRCode                                                |
| qrcode_original_path | O Path para colar diretamente no aplicativo do Banco e realizar o agamento |



##### Informações importantes

**Tempo Expiração**: O tempo de expiração do QRCode vem configurado default em 24h (1440 minutos). Para configura-lo você precisa acessar o [Portal](https://intermediador.yapay.com.br/settings/sales) da Yapay -> Configurações -> Transação de vendas -> Duração do QRCode (PIX). A transação PIX que está com o status Aguardando Pagamento que está com o QRCode expirado, nós realizamos o Cancelamento da transação no minuto 40 de cada hora. 


**Cancelamento de transação PIX**: O cancelamento da transação, via API ou Portal, com a forma de pagamento PIX é somente com o status AGUARDANDO PAGAMENTO. Não é possível cancelar transação PIX com o status APROVADA. 


**Recebível**: O recebimento das transações PIX é feito automático 2x ao dia.


> Valor mínimo de transação de PIX é R$ 2,00


Altere o nó payment para:

```javascript
	    "payment":{  
	       "payment_method_id":"27",
	       "split": "1"
	    }
```


## Enviando uma transação PIX

Para esta integração, deverá ser feito <span class="post">POST</span> uso da API a seguir:

| Endereço para Integração |                                                                              |
|--------------------------|----------------------------------------------------------------------------|
| Ambiente de Testes       | https://api.intermediador.sandbox.yapay.com.br/api/v3/transactions/payment |
| Ambiente de Produção     | https://api.intermediador.yapay.com.br/api/v3/transactions/payment |
| Protocolo                | Rest/HTTP                                                                  |

> É necessario utilizar o Protocolo de Criptografia TLS na versão 1.2. 

Abaixo você consegue visualizar um exemplo em cURL da criação de uma Transação em PIX:

> **Exemplo de criação de Transação com PIX**

```bash
    curl  --request POST \
          --url 'https://api.intermediador.sandbox.yapay.com.br/api/v3/transactions/payment' \
          --header 'Content-Type: application/json' \
          --data '{  
                "token_account":"SEU_TOKEN_AQUI",
                "customer":{  
                "contacts":[  
                    {  
                    "type_contact":"H",
                    "number_contact":"1133221122"
                    },
                    {  
                    "type_contact":"M",
                    "number_contact":"11999999999"
                    }
                ],
                "addresses":[  
                    {  
                    "type_address":"B",
                    "postal_code":"17000-000",
                    "street":"Av Esmeralda",
                    "number":"1001",
                    "completion":"A",
                    "neighborhood":"Jd Esmeralda",
                    "city":"Marilia",
                    "state":"SP"
                    }
                ],
                "name":"Wanda Maximoff",
                "birth_date":"21/05/1941",
                "cpf":"50235335142",
                "email":"wanda@avengers.com"
                },
                "transaction_product":[  
                {  
                    "description":"Camiseta Tony Stark",
                    "quantity":"1",
                    "price_unit":"130.00",
                    "code":"1",
                    "sku_code":"0001",
                    "extra":"Informação Extra"
                }
                ],
                "transaction":{  
                "shipping_type":"Sedex",
                "shipping_price":"12",
                "url_notification":"http://www.loja.com.br/notificacao",
                "free":""
              },
              "transaction_trace": {
                 "estimated_date": "02/04/2022"
              },
                "payment":{  
                  "payment_method_id":"27",  
                  "split":"1"
                }
            }'

```


> Resposta da API

A API de Transações retorna a resposta em <span class="post">JSON</span>.

Exemplo de resposta com sucesso, se baseando no envio do exemplo acima:


```javascript
{
   "message_response":{
      "message":"success"
   },
   "data_response":{
      "transaction":{
         "order_number":"99509",
         "free":"Campo Livre",
         "transaction_id":599509,
         "status_name":"Aguardando Pagamento",
         "status_id":4,
         "token_transaction":"08b79a139d541003d88fcad8e415c63",
         "payment":{
            "price_payment":"142.0",
            "price_original":"142.0",
            "payment_response":"",
            "url_payment":"https://intermediador-sandbox.yapay.com.br/orders/pix/c0192199748828323ff07d0d1c409885",
            "qrcode_path": "https://dzpxyxks1bfmb.cloudfront.net/production/bs2/71885394_qrcode.svg",
	"qrcode_original_path": "00020101021226910014BR.GOV.BCB.PIX2569api-pix-h.bancobs2.com.br/spi/v2/61d4f657-0120-44c2-b51a-843425bb4572520400005303986540560.005802BR5905Yapay6014Belo Horizonte61083038040362070503***6304DE06",
	"tid":"",
            "split":1,
            "payment_method_id":27,
            "payment_method_name":"Pix",
            "linha_digitavel":""
         },
         "customer":{
            "name":"Wanda Maximoff",
            "company_name":"",
            "trade_name":"",
            "cpf":"35502074846",
            "cnpj":""
         }
         }
      }
   }
}
```
