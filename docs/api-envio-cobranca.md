# API Envio de Cobrança

<span class="post">POST</span><span class="beforePost">/api/transaction_charges/create</span>

A Yapay Intermediador fornece uma ferramenta poderosa para pessoas que desejam enviar um link com o envio de cobrança. Utilizando essa API o cliente receberá um e-mail com o valor para realizar o pagamento. 

É possível enviar a quantidade de produtos editavel ou não.


| Endereço para Integração |                                                                               |
|--------------------------|-------------------------------------------------------------------------------|
| Ambiente de Testes       | https://api.intermediador.sandbox.yapay.com.br/api/transaction_charges/create |
| Ambiente de Produção     | https://api.intermediador.yapay.com.br/api/transaction_charges/create         |
| Protocolo                | Rest/HTTP                                                                     |

> É necessario utilizar o Protocolo de Criptografia TLS na versão 1.2. 

# Códigos de Exemplo


```javascript
    {
        "access_token": "SEU_ACCESS_TOKEN",
        "email_customer": "stephen.strange@avengers.com",               
            
        "transaction_product":[  
            {  
                "description": "Infinity Stone",
                "quantity": "1",
                "price_unit": "1500.00",
                "code": "1",
                "shipping": "0",
                "edit": "true"
            }
        ]   
    }
```


# Resposta da API

> Exemplo de resposta em XML com `sucesso` baseando no envio do exemplo:

```xml
    <transaction_charge>
        <message_response>
            <message>success</message>
        </message_response>
        <data_response>
            <transaction_charge_id type="integer">711</transaction_charge_id>
            <customer_email>stephen.strange@avengers.com</customer_email>
            <created_at>28/12/2018</created_at>
            <tmp_transaction>
                <order_number>1546017563</order_number>
                <seller_name>Thanos de Titã</seller_name>
                <seller_email>thanos@tita.com</seller_email>
                <price type="decimal">1500.0</price>
                <status_id type="integer">4</status_id>
                <edit type="boolean">true</edit>
                <token_transaction>t5ac99753a193ea77226210084ee820cc</token_transaction>
                <url_payment>https://tc.intermediador.sandbox.yapay.com.br/payment/car/</url_payment>
                <description>Infinity Stone</description>
            </tmp_transaction>
        </data_response>
    </transaction_charge>
```


> Exemplo de resposta com `erro` baseando no envio do exemplo:


```xml
    <transaction_charge>
        <message_response>
            <message>error</message>
        </message_response>
        <error_response>
            <general_errors type="array">
                <general_error>
                    <code>060003</code>
                    <message>Token de acesso inválido ou expirado.</message>
                </general_error>
            </general_errors>
        </error_response>
    </transaction_charge>
```



As mensagens de erros retornados pela API estão listadas na tabela abaixo:

| Código    |  Mensagem                                   |
|-----------|---------------------------------------------|
| 060003	| Token inválido ou não encontrado            |
| 038009    | E-mail do cliente é inválido                |


# Tabela de Parâmetros

Para a integração via <span class="post">POST</span>, segue abaixo os dados necessários para envio:

| Dados de Entrada                    |	Obrig.  |	Descrição                                            |
|-------------------------------------|---------|--------------------------------------------------------|
| access_token                        |	Sim     | Token de acesso                                        |
| session_id                          |	Não	    | ID do Cliente                                          |
| email_customer                      |	Sim     | E-mail do cliente                                      |
| order_number                        | Não     | Número do Pedido                                       |
| max_split_transaction               | Não     | Valor máximo de parcela                                |
| available_payment_methods           | Não     | Formas de pagamento disponíveis para essa compra. Enviando null aceitará todas [(Tabela)](https://intermediador.dev.yapay.com.br/#/tabelas?id=tabela-3-formas-de-pagamento)   
| transaction_product[][description]  | Sim     | Descrição do Produto                                   |
| transaction_product[][price_unit]   | Sim     | Preço                                                  |
| transaction_product[][type_product] | Não     | Tipo do produto (S = serviço / Vazio = normal)         |
| transaction_product[][shipping]     | Não     | Usar frete 0-Não, 1-Sim                                |
| transaction_product[][edit]         | Não     | Permite edição da quantidade do produto. True ou False |

