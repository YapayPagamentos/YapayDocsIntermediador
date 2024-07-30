## Bolepix


A forma de pagamento **Bolepix** na Vindi já está disponível para todos na criação de transações pela API de Transação. Com essa forma de pagamento é possível criar um boleto com um QR Code PIX para pagamento. Ou seja, o permitindo que o pagamento dessa transação seja feito por PIX ou Boleto.

Para utilizar é simples, você precisa passar o `payment_method_id` igual a `28`. No response da API vem os seguintes campos:

| Campo                | Descrição campo                                                            |
|----------------------|----------------------------------------------------------------------------|
| url_payment          | URL de Pagamento para direcionar o cliente para visualizar o boleto        |
| qrcode_path          | URL da imagem SVG do QRCode                                                |
| qrcode_original_path | O Path para colar diretamente no aplicativo do Banco e realizar o agamento |



##### Informações importantes

**Tempo Expiração**: O tempo de expiração do QRCode vem configurado default em 24h (1440 minutos). Para configura-lo você precisa acessar o [Portal](https://intermediador.yapay.com.br/settings/sales) da Vindi -> Configurações -> Transação de vendas -> Duração do QRCode (PIX). A transação PIX que está com o status Aguardando Pagamento que está com o QRCode expirado, nós realizamos o Cancelamento da transação no minuto 40 de cada hora. 


**Recebível**: O recebimento das transações PIX é feito automático 2x ao dia.

**Contingência**: Por enquanto, não temos contingência desta forma de pagamento. Caso ocorra erro de criação, deve ser criado uma nova transação.


Altere o nó payment para:

```javascript
	    "payment":{  
	       "payment_method_id":"28",
	       "split": "1"
	    }
```


## Enviando uma transação Bolepix

Para esta integração, deverá ser feito <span class="post">POST</span> uso da API a seguir:

| Endereço para Integração |                                                                              |
|--------------------------|----------------------------------------------------------------------------|
| Ambiente de Testes       | https://api.intermediador.sandbox.yapay.com.br/api/v3/transactions/payment |
| Ambiente de Produção     | https://api.intermediador.yapay.com.br/api/v3/transactions/payment |
| Protocolo                | Rest/HTTP                                                                  |

> É necessario utilizar o Protocolo de Criptografia TLS na versão 1.2. 

Abaixo você consegue visualizar um exemplo em cURL da criação de uma Transação em Bolepix:

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
                  "payment_method_id":"28",  
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
                "url_payment": "https://intermediador-sandbox.yapay.com.br/orders/bolepix/b047ff173b88f4dd3387a79a484f3756",
                "qrcode_path": "https://d3qiiqeqvrl56p.cloudfront.net/sandbox/2024/07/30/itau/N101240656_qrcode.svg",
                "qrcode_original_path": "00020101021226860014BR.GOV.BCB.PIX2564spi-h.itau.com.br/pix/qr/v2/e8772e8f-3e31-4766-831c-c3ce8f453b635204000053039865802BR5920CARVALHEIRA GERALDES6009SAO PAULO62070503***63048DAC",
	"tid":"",
            "split":1,
            "payment_method_id":28,
            "payment_method_name":"Bolepix",
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

## Exemplo de Bolepix


![Obtendo o Token de Integração Vindi](/images/bolepix_vindi.png "Bolepix Vindi")
