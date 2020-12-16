# Boleto

Também é disponibilizada a funcionalidade de pagamentos com o meio de pagamento Boleto pela API de Transação. É de extrema importância a utilização do nosso fingerprint, abaixo você verá uma explicação mais detalhada sobre isso.

Você pode visualizar os IDs para as formas de pagamento na nossa <a href="/#/tabelas?id=tabela-3-formas-de-pagamento">Tabela Auxiliar 3 - Formas de Pagamento</a>

Basta você alterar o nó payment para:

```javascript
	    "payment":{  
	       "payment_method_id":"6"
	    }
```	    

No parâmetro `payment[billet_date_expiration]` você pode enviar a data de vencimento do boleto, caso não queira utilizar a padrão das contas Yapay.

Adicionando no nó payment:

```javascript
      "payment":{  
         "payment_method_id":"6",
         "billet_date_expiration": "15/03/2018"
      }
```

> Valor mínimo de transação de boleto é R$ 1,00


## Enviando uma transação


Para esta integração, deverá ser feito <span class="post">POST</span> uso da API a seguir:

| Endereço para Integração |                                                                             |
|--------------------------|----------------------------------------------------------------------------|
| Ambiente de Testes       | https://api.intermediador.sandbox.yapay.com.br/api/v3/transactions/payment |
| Ambiente de Produção     | https://api.intermediador.yapay.com.br/api/v3/transactions/payment |
| Protocolo                | Rest/HTTP                                                                  |

> É necessario utilizar o Protocolo de Criptografia TLS na versão 1.2. 

Abaixo você consegue visualizar um exemplo em cURL da criação de uma Transação em Boleto:


> **Exemplo de criação de Transação com Boleto**

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
                "name":"Stephen Strange",
                "birth_date":"21/05/1941",
                "cpf":"50235335142",
                "email":"stephen.strange@avengers.com"
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
                "available_payment_methods":"2,3,4,5,6,7,14,15,16,18,19,21,22,23",
                "customer_ip":"127.0.0.1",
                "shipping_type":"Sedex",
                "shipping_price":"12",
                "price_discount":"",
                "url_notification":"http://www.loja.com.br/notificacao",
                "free":"Campo Livre"
              },
              "payment":{  
                "payment_method_id":"6"
              }
            }'

```

> **Exemplo de criação de Transação PHP + curl**

```php
  function callAPI($method, $url, $data){
     $curl = curl_init();

     switch ($method){
        case "POST":
           curl_setopt($curl, CURLOPT_POST, 1);
           if ($data)
              curl_setopt($curl, CURLOPT_POSTFIELDS, $data);
           break;
        case "PUT":
           curl_setopt($curl, CURLOPT_CUSTOMREQUEST, "PUT");
           if ($data)
              curl_setopt($curl, CURLOPT_POSTFIELDS, $data);                
           break;
        default:
           if ($data)
              $url = sprintf("%s?%s", $url, http_build_query($data));
     }

     // OPTIONS:
     curl_setopt($curl, CURLOPT_URL, $url);
     curl_setopt($curl, CURLOPT_HTTPHEADER, array('Content-Type: application/json'));
     curl_setopt($curl, CURLOPT_RETURNTRANSFER, 1);
     curl_setopt($curl, CURLOPT_HTTPAUTH, CURLAUTH_BASIC);

     // EXECUTE:
     $result = curl_exec($curl);
     if(!$result){die("Connection Failure");}
     curl_close($curl);
     return $result;
  }

  // DADOS DO PEDIDO
  $data["token_account"] = "SEU_TOKEN_AQUI";

  $data["customer"]["contacts"][1]["type_contact"] = "H";
  $data["customer"]["contacts"][1]["number_contact"] = "1133221122";

  $data["customer"]["addresses"][1]["type_address"] = "B";
  $data["customer"]["addresses"][1]["postal_code"] = "17516000";
  $data["customer"]["addresses"][1]["postal_code"] = "17000-000";
  $data["customer"]["addresses"][1]["street"] = "Av Esmeralda";
  $data["customer"]["addresses"][1]["number"] = "1001";
  $data["customer"]["addresses"][1]["neighborhood"] = "Jd Esmeralda";
  $data["customer"]["addresses"][1]["city"] = "Marilia";
  $data["customer"]["addresses"][1]["state"] = "SP";

  $data["customer"]["name"] = "Stephen Strange";
  $data["customer"]["cpf"] = "74279789517";
  $data["customer"]["email"] = "teste.teste@teste.com";

  $data["transaction_product"][1]["description"] = "Camiseta Tony Stark";
  $data["transaction_product"][1]["quantity"] = "1";
  $data["transaction_product"][1]["price_unit"] = "130.00";

  $data["transaction"]["shipping_type"] = "Sedex";
  $data["transaction"]["shipping_price"] = "";
  $data["transaction"]["url_notification"] = "";

  $data["payment"]["payment_method_id"] = "6";
  $data["payment"]["split"] = "1";

  $data_string = json_encode($data);

  $get_data = callAPI('POST', 'URL_END_POINT', $data_string );
```



> Resposta da API

A API de Transações retorna a resposta em JSON. Observe que no retorno você recebe dentro do nó payment o campo `url_payment`, com esse campo você pode fazer o redirecionamento para o cliente realizar o pagamento. 

Exemplo de resposta com sucesso baseando no envio do exemplo acima:


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
            "token_transaction": "cb22c716c80ddbaa16f8b8dbc49302a2",
            "payment": {
                "price_payment": "142.0",
                "price_original": "142.0",
                "payment_response": "",
                "url_payment": "https://tc.intermediador.sandbox.yapay.com.br/payment/billet/fc0579d4217be829b06755078e26a493",
                "split": 3,
                "payment_method_id": 6,
                "payment_method_name": "Boleto Bancário",
                "linha_digitavel": "123123123123123131232131232131313211231321321"
            },
            "customer": {
                "name": "Stephen Strange",
                "company_name": "",
                "trade_name": "",
                "cnpj": ""
            }
        }
    }
}
```




