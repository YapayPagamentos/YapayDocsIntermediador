# Entendendo o Fingerprint


Através do CPF do cliente é feita a consulta pela existência do seu cadastro e então as transações são atreladas ao mesmo. Caso não exista uma conta, o sistema irá criar uma nova conta com os dados que forem submetidos na integração.


> **O que é antifraude?**


Um sistema de antifraude é acionado devido ao aumento de vazamento de informações. Essas informações são capturadas por hackers que são especializados em roubo desses dados na internet. 

Com esses problemas surgiram os sistemas de antifraude, que analisam as informações no momento da compra, verificando algumas possibilidades de uma possível fraude.

> **O que é fingerprint?**


O fingerprint é um script criado em javascript que grava vários dados para que seja realizada a analise das informações. Essas informações são enviadas no momento do POST da transação.


> **Como utilizar o fingerprint?**


É importante que você adicione algumas informações para que a coleta de informações realizadas pelo fingerprint funcione corretamente. No código de exemplo ao lado, você consegue visualizar de uma maneira bem simplicada o funcionamento.


> **Em que lugar da página eu coloco o fingerprint?**


**1-** No momento que você criou o formulário para envio das informações da transação, você deve adicionar o atributo `data-yapay="payment-form"`. Incluindo esse atributo será criado um input do tipo `hidden`, com o valor do parâmetro `finger_print` que deve ser enviado junto com os parâmetros de criação na API de Transação. Exemplo de form em HTML:

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
    <script>window.yapay.FingerPrint({ env: 'sandbox' });</script>
```
> A TAG `env` quando não informada estará apontando para o ambiente Produção da Yapay. Portanto é necessário informar `env: 'sandbox'` para os testes em SANDBOX.

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

### É de extrema importância incluir o fingerprint em **TODOS** os meios de pagamento.
 
