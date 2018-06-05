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
                $data["customer"]["addresses"][1]["street"] = "Av Themyscira";
                $data["customer"]["addresses"][1]["number"] = "1001";
                $data["customer"]["addresses"][1]["neighborhood"] = "Jd das Rochas";
                $data["customer"]["addresses"][1]["city"] = "Themyscira";
                $data["customer"]["addresses"][1]["state"] = "SP";

                $data["customer"]["name"] = "Diana Prince";
                $data["customer"]["cpf"] = "55928871830";
                $data["customer"]["email"] = "dianeprince@amazonas.br";

                $data["transaction_product"][1]["description"] = "Camiseta Wonder Woman";
                $data["transaction_product"][1]["quantity"] = "1";
                $data["transaction_product"][1]["price_unit"] = "1.00";

                $data["transaction"]["shipping_type"] = "Sedex";
                $data["transaction"]["shipping_price"] = "";
                $data["transaction"]["url_notification"] = "";
                $data["transaction"]["customer_ip"] = "127.0.0.1";

                $data["payment"]["payment_method_id"] = "3";
                $data["payment"]["card_name"] = "DIANA PRINCE";
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
	       "card_name": "DIANA PRINCE",
	       "card_number": "4111111111111111",
	       "card_expdate_month": "01",
	       "card_expdate_year": "2021",
	       "card_cvv": "644",
	       "split": "1"
	    }
```


## Envindo uma transação

Abaixo você consegue visualizar um exemplo em JSON da criação de uma Transação em Cartão de Crédito:

> **Exemplo em JSON**

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
                    "street":"Av Themyscira",
                    "number":"1001",
                    "completion":"A",
                    "neighborhood":"Jd das Rochas",
                    "city":"Themyscira",
                    "state":"SP"
                  }
                ],
                "name":"Diana Prince",
                "birth_date":"21/05/1941",
                "cpf":"50235335142",
                "email":"email@cliente.com.br"
              },
              "transaction_product":[  
                {  
                  "description":"Camiseta Wonder Woman",
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
                "card_name":"DIANA PRINCE",
                "card_number":"4111111111111111",
                "card_expdate_month":"01",
                "card_expdate_year":"2021",
                "card_cvv":"644",
                "split":"1"
              }
            }'

```


## Tabela de Campos

Para a integração via <span class="post">POST</span>, segue abaixo os dados necessários para envio:

| Dados de Entrada                         |  Obrig.  | Formato / Tam. Max   | Descrição                                                  |
|------------------------------------------|----------|----------------------|------------------------------------------------------------|
| token_account                            |   Sim    |  Texto /20           |  Token de identificação do vendedor                      |
| customer[name]                           |   Sim    |  Texto /100          |  Nome do Comprador                                       |
| customer[cpf]                            |   Sim    |  Texto /14           |  CPF do Comprador                                        |
| customer[email]                          |   Sim    |  Texto /100          |  E-mail do Comprador                                     |
| customer[trade_name]                     |   Não    |  Texto /100          |  Nome Fantasia do Comprador                              |
| customer[company_name]                   |   Não    |  Texto /100          |  Razão Social do Comprador                               |
| customer[cnpj]                           |   Não    |  Texto /18           |  CNPJ do Comprador                                       |
| customer[inscricao_municipal]            |   Não    |  Texto /20           |  Inscrição Municipal do Comprador                        |
| customer[contacts][][type_contact]       |   Sim    |  Texto /1            |  Tipo do Contato <sup>1</sup> (Tabela 1)                 |
| customer[contacts][][number_contact]     |   Sim    |  Texto /11           |  Número do telefone do Comprador                         |
| customer[addresses][][type_address]      |   Sim    |  Texto /1            |  Tipo do Endereço <sup>1</sup> (Tabela 2)                |
| customer[addresses][][postal_code]       |   Sim    |  Texto /8            |  CEP do endereço do Comprador                            |
| customer[addresses][][street]            |   Sim    |  Texto /120          |  Nome da rua do Comprador                                |
| customer[addresses][][number]            |   Sim    |  Texto /10           |  Número do endereço do Comprador                         |
| customer[addresses][][neighborhood]      |   Sim    |  Texto /100          |  Bairro do endereço do Comprador                         |
| customer[addresses][][completion]        |   Não    |  Texto /100          |  Complemento do endereço do Comprador                    |
| customer[addresses][][city]              |   Sim    |  Texto /120          |  Cidade do endereço do Comprador                         |
| customer[addresses][][state]             |   Sim    |  Texto /2            |  Estado do endereço do Comprador                         |
| customer[birth_date]                     |   Não    |  Data / 10           |  Data de aniversário do Comprador                        |
| transaction[available_payment_methods]   |   Não    |  Texto /20           |  Meios de Pagamento disponíveis <sup>2</sup> (Tabela 3)  |
| transaction[order_number]                |   Não    |  Texto /2            |  Número do pedido                                        |
| transaction[customer_ip]                 |   Sim    |  Texto /15           |  IP do Comprador                                         |
| transaction[shipping_type]               |   Não    |  Texto /100          |  Tipo do envio                                           |
| transaction[shipping_price]              |   Não    |  Decimal / 11        |  Preço de Envio. Formato: 0.00                           |
| transaction[price_discount]              |   Não    |  Decimal / 11        |  Valor do desconto. Formato: 0.00                        |
| transaction[price_additional]            |   Não    |  Decimal / 11        |  Valor adicional. Formato: 0.00                          | 
| transaction[url_notification]            |   Não    |  Texto /255          |  URL de Notificação Automática de Status<sup>5</sup>     |
| transaction[free]                        |   Não    |  Texto /200          |  Campo Livre                                             |
| transaction[sub_store]                   |   Não    |  Texto /20           |  Sub-Loja                                                |
| transaction_product[][description]       |   Sim    |  Texto /100          |  Nome do produto <sup>1</sup>                            |
| transaction_product[][quantity]          |   Sim    |  Número / 3          |  Quantidade do item do produto                           |
| transaction_product[][price_unit]        |   Sim    |  Decimal / 11        |  Valor unitário. Formato: 0.00                           |
| transaction_product[][code]              |   Não    |  Texto /10           |  Código do produto                                       |
| transaction_product[][sku_code]          |   Não    |  Texto /50           |  Código SKU do produto                                   |
| transaction_product[][extra]             |   Não    |  Texto /100          |  Campo Livre do produto                                  |
| transaction[max_split_transaction]       |   Não    |  Número /10          |  Número máximo de parcelas                                  |
| payment[payment_method_id]               |   Sim    |  Texto /2            |  Forma de Pagamento                                      |
| payment[split]                           |   Sim    |  Texto /2            |  Número de parcelas (01 a 12)                            |
| payment[person_card_id]                  |   Não    |  Texto /100          |  Código do cartão cadastrado em nosso cofre <sup>3</sup> |
| payment[card_name]                       |   Não    |  Texto /100          |  Nome impresso no cartão                                 |
| payment[card_number]                     |   Não    |  Número /20          |  Número do cartão                                        |
| payment[card_expdate_month]              |   Não    |  Número /2           |  Mês de vencimento do cartão                             |
| payment[card_expdate_year]               |   Não    |  Número / 4          |  Ano de vencimento do cartão                             |
| payment[card_cvv]                        |   Não    |  Número /3           |  Código de segurança do cartão                           |
| payment[billet_date_expiration]          |   Não    |  Data / 10           |  Data de Vendimento do Boleto                            |
| affiliates[][account_email]              |   Não    |  Texto / 100         |  Email do afiliado da transação                          |
| affiliates[][percentage]                 |   Não    |  Número / 3          |  Percentual de repasse ao afiliado <sup>4</sup>          |
| affiliates[][commission_amount]          |   Não    |  Decimal / 11        |  Valor de repasse ao afiliado <sup>5</sup>               |
| reseller_token                           |   Não    |  Texto               |  Valor de repasse ao afiliado <sup>6</sup>               |
| finger_print                             |   Não    |  Texto /100          |  Token gerado pelo FingerPrint <sup>7</sup>              |


> <sup>1</sup> Note que nas informações acima que alguns dados possuem uma característica diferente, tendo um elemento [] dentro de sua formatação. Isso ocorre justamente para permitir que sejam enviados diversos itens na mesma requisição. 


> <sup>2</sup> O parâmetro `transaction[available_payment_methods]` permite que sejam enviados os códigos de meios de pagamento que poderão ser disponibilizados no processo de recobrança de transações. Os códigos deverão ser enviados separados por vírgula (,). Esse campo é útil quando a loja oferece uma condição especial de pagamento, por exemplo Desconto de 10% no Boleto Bancário. Assim deve-se enviar apenas o código do boleto bancário para que seja disponibilizada somente esta forma de pagamento no processo de recobrança.


> <sup>3</sup> O parâmetro `payment[person_card_id]` é informado com o código do cartão de crédito cadastrado em nossos cofres. Esse código é vinculado ao Vendedor e ao Cliente do Cartão de Crétido.


> <sup>4</sup> O parâmetro `affiliates[][]` é informado quando é necessário que seja feito Repasse Automático ao Revendedor. Essa opção é utilizada na Integração com Marketplace.


> <sup>5</sup> O parâmetro `transaction[url_notification]` é informado para comunicar a sua aplicação a cada alteração de status de uma transação. Saiba mais em Notificação Automática de Status.


> <sup>6</sup> O parâmetro `reseller_token` é informado para comunicar que a transação é vinculada a um revendedor. Dessa forma todas as transações que são enviadas com esse parâmetro ficam vinculadas ao revendedor.


> <sup>7</sup> O parâmetro `finger_print` é informado por um script Javascript que faz uma coleta de dados e realiza a analise das informações disponíveis publicamente na máquina. Dessa forma é realizada a Análise de Risco.
