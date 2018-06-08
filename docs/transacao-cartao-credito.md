## Fingerprint


Através do CPF do cliente é feita a consulta pela existência do seu cadastro e então as transações são atreladas ao mesmo. Caso não exista uma conta, o sistema irá criar uma nova conta com os dados que forem submetidos na integração. Para esta integração, deverá ser feito uso da API a seguir:


> **O que é antifraude?**


Um sistema de antifraude é acionado devido ao aumento de vazamento de informações. Essas informações são capturadas por hackers que são especializados em roubo desses dados na internet. 

Com esses problemas surgiram os sistemas de antifraude, que analisam as informações no momento da compra, verificando algumas possibilidades de uma possível fraude.

> **O que é fingerprint?**


O fingerprint é um script criado em javascript que grava vários dados para que seja realizada a analise das informações. Essas informações são enviadas no momento do POST da transação.


> **Como utilizar o fingerprint?**


É importante que você adicione algumas informações para que a coleta de informações realizadas pelo fingerprint funcione corretamente. No código de exemplo ao lado, você consegue visualizar de uma maneira bem simplicada o funcionamento.


> **Em que lugar da página eu cologo o fingerprint?**


**1-** No momento que você criou o formulário para envio das informações da transação, você deve adiionar a tag `data-yapay="payment-form"`. Incluindo essa tag será criado um input do tipo `hidden`, com o valor do parâmetro `finger_print` que deve ser enviado junto com os parâmetros de criação na API de Transação. Exemplo de form em HTML:

```html
    <html>
        <body>
            <form action="acao.php" method="post"  data-yapay="payment-form">
                <input type="submit" name="submit" value="Submit" />
            </form>
        </body>
    </html>
```

**2-** No momento do envio para a API de Transação, você deve adicionar o parâmetro `finger_print`. Exempĺo do código em PHP abaixo:

```php
    <?php
        
        $data["finger_print"] = $_POST['finger_print'];
                
    ?>
```


**3-** Você deve incluir um script no processamento da transação (na página de checkout), no início da página de finalização da compra. Segue abaixo código do script:

```html
 <script src="https://static.traycheckout.com.br/js/finger_print.js" type="text/javascript"></script>
```

Também deve realizar a chamada do plugin, no final da mesma página. Essa chamada acionará o fingerprint para que seja realizada a coleta e analise de dados. Conforme código javascript abaixo:

```php
    <script type="text/javascript">
        jQuery(document).FingerPrint();
    </script>
```

Após esses procedimentos é enviado juntamente com o JSON de requisição o parâmetro `finger_print`, onde conseguimos realizar a analise antifraude.


> **O fingerprint funciona nos ambientes `SANDBOX` e `PRODUÇÃO`.**

Código de exemplo para utilizar o Fingerprint:

```php
        if(isset($_POST['submit']))
        {
                $data["token_account"] = "SEU_TOKEN_AQUI";
                $data["finger_print"] = $_POST['finger_print'];

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
                $data["customer"]["cpf"] = "55928871830";
                $data["customer"]["email"] = "stephen.strange@avengers.com";

                $data["transaction_product"][1]["description"] = "Camiseta Tony Stark";
                $data["transaction_product"][1]["quantity"] = "1";
                $data["transaction_product"][1]["price_unit"] = "130.00";

                $data["transaction"]["shipping_type"] = "Sedex";
                $data["transaction"]["shipping_price"] = "";
                $data["transaction"]["url_notification"] = "";
                $data["transaction"]["customer_ip"] = "127.0.0.1";

                $data["payment"]["payment_method_id"] = "3";
                $data["payment"]["card_name"] = "STEPHEN STRANGE";
                $data["payment"]["card_number"] = "4111111111111111";
                $data["payment"]["card_expdate_month"] = "04";
                $data["payment"]["card_expdate_year"] = "2021";
                $data["payment"]["card_cvv"] = "532";
                $data["payment"]["split"] = "1";

                $url = "https://api.intermediador.sandbox.yapay.com.br/api/v3/transactions/payment";

                ob_start();

                $ch = curl_init();
                curl_setopt($ch, CURLOPT_URL, $url);
                curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "POST");
                curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($data));
                curl_setopt($ch, CURLOPT_HTTPHEADER, array('Content-Type: application/json'));

                curl_exec($ch);

                // JSON de retorno
                $resposta = json_decode(ob_get_contents());
                $code = curl_getinfo($ch, CURLINFO_HTTP_CODE);

                ob_end_clean();
                curl_close($ch);

                if($code == "201"){
                    //Tratamento dos dados de resposta da consulta.
                }else{
                    //Tratamento das mensagens de erro
                }
        }
        ?>
        
        <html>
            <head>
                <script src="https://code.jquery.com/jquery-3.2.1.js" integrity="sha256-DZAnKJ/6XZ9si04Hgrsxu/8s717jcIzLy3oi35EouyE=" crossorigin="anonymous"></script>
                <script src="https://static.traycheckout.com.br/js/finger_print.js" type="text/javascript"></script>
            </head>
            <body>
                <form action="index.php" method="post"  data-yapay="payment-form">
                    <input type="submit" name="submit" value="Enviar Post" />
                </form>
            </body>

            <script type="text/javascript">
                jQuery(document).FingerPrint().getFingerPrint();                
            </script>
        </html>

```


## Dados do Cartão de Crédito


Uma das funcionalidades do Yapay Intermediador é criação de transações pela API de Transação com o meio de pagamento **Cartão de Crédito**. Essa transação, dependendo da Tabela que você se encaixa é feito uma analise de antifraude.

É de extrema importância a utilização do nosso fingerprint, abaixo você verá uma explicação mais detalhada sobre isso.

Basta você alterar o nó payment para:

```javascript
	    "payment":{  
	       "payment_method_id":"3",
	       "card_name": "STEPHEN STRANGE",
	       "card_number": "4111111111111111",
	       "card_expdate_month": "01",
	       "card_expdate_year": "2021",
	       "card_cvv": "644",
	       "split": "1"
	    }
```


## Enviando uma transação

Para esta integração, deverá ser feito <span class="post">POST</span> uso da API a seguir:

| Endereço para Integração                                                                              |
|--------------------------|----------------------------------------------------------------------------|
| Ambiente de Testes       | https://api.intermediador.sandbox.yapay.com.br/api/v3/transactions/payment |
| Ambiente de Produção     | https://api.intermediador.yapay.com.br/api/v3/transactions/payment |
| Protocolo                | Rest/HTTP                                                                  |

Abaixo você consegue visualizar um exemplo em cURL da criação de uma Transação em Cartão de Crédito:

> **Exemplo de criação de Transação com Cartão de Crédito**

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
                "payment_method_id":"3",
                "card_name":"STEPHEN STRANGE",
                "card_number":"4111111111111111",
                "card_expdate_month":"01",
                "card_expdate_year":"2021",
                "card_cvv":"644",
                "split":"1"
              }
            }'

```


> Resposta da API

A API de Transações retorna a resposta em JSON.

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
                "price_payment": "147.69",
                "price_original": "142.0",
                "payment_response": "Autorização aprovada",
                "url_payment": "",
                "tid": "10347871500026BF1001",
                "split": 3,
                "payment_method_id": 3,
                "payment_method_name": "Visa",
                "linha_digitavel": null
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

