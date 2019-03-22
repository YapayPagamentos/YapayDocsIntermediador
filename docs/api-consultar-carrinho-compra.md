# API Consultar Carrinho de Compra

<span class="post">POST</span><span class="beforePost">/v1/tmp_transactions/get</span>


Com a API de Consulta de Carrinho de Compra você consegue visualizar se a transação temporária criada através da **API Carrinho de Compra** converteu para uma transação definitiva.


| Endereço para Integração |                                                                              |
|--------------------------|------------------------------------------------------------------------------|
| Ambiente de Testes       | https://api.intermediador.sandbox.yapay.com.br/v1/tmp_transactions/get       |
| Ambiente de Produção     | https://api.intermediador.yapay.com.br/v1/tmp_transactions/get                |
| Protocolo                | Rest/HTTP                                                                    |

> É necessario utilizar o Protocolo de Criptografia TLS na versão 1.2. 

> **Observação:** Note que no retorno da API tem o campo `<payment>`, esse campo é o parâmetro o `token_transaction` da transação definitiva. Nesse caso foi realizado o pagamento para esta transação temporária. Caso não tenha pagamento será retornado `<payment nil="true"/>`. Com o `token_transaction` da transação definitiva você consegue realizar uma consulta na <a href="/#/api-consultar-transacao" target="_blank">API de Consulta de Transação</a> e manipular as informações da forma que precisar!

# Códigos de Exemplo


```javascript
    {
        "token_account": "SEU_TOKEN",
        "token_transaction": "3cfbb284fab20acbd0754feb4a1de435"
    }
```


# Resposta da API

> Exemplo de resposta em XML com `sucesso` baseando no envio do exemplo:

```xml
    <tmp_transaction>
        <message_response>
            <message>success</message>
        </message_response>
        <data_response>
            <token_transaction>c543a7c7874c71882e6ad8f12f3e46</token_transaction>
            <url_car>https://tc.intermediador.sandbox.yapay.com.br/payment/car/v1/</url_car>
            <transaction_products type="array">
                <transaction_product>
                    <code>1</code>
                    <img nil="true"/>
                    <sku_code nil="true"/>
                    <description>Camiseta Wonder Woman</description>
                    <extra nil="true"/>
                    <price_unit type="decimal">130.0</price_unit>
                    <quantity type="decimal">1.0</quantity>
                    <weight nil="true"/>
                    <id type="integer">8894</id>
                    <type_product nil="true"/>
                </transaction_product>
            </transaction_products>
        </data_response>
    </tmp_transaction>
```


> Exemplo de resposta com `erro` baseando no envio do exemplo:


```xml
    <tmp_transaction>
        <message_response>
            <message>error</message>
        </message_response>
        <error_response>
            <general_errors type="array">
                <general_error>
                    <code>001001</code>
                    <message>Token inválido ou não encontrado</message>
                </general_error>
            </general_errors>
        </error_response>
    </tmp_transaction>
```


As mensagens de erros retornados pela API estão listadas na tabela abaixo:

| Código   |  Mensagem                                  |
|----------|--------------------------------------------|
| 038002   | Transação temporária não encontrada        |



# Tabela de Parâmetros

Para a integração via <span class="post">POST</span>, segue abaixo os dados necessários para envio:

| Dados de Entrada  |  Obrig.  | Descrição                                                                                     |
|-------------------|----------|-----------------------------------------------------------------------------------------------|
| token_account     | Não      | Token da conta da Loja                                                                        |
| token_transaction | Sim      | Token da Transação temporária                                                                 |
| order_number      | Não      | Número do Pedido da Transação temporária (É o mesmo número de pedido da Transação Definitiva) |

