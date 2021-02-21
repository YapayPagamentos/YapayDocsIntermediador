# API Carrinho de Compra

<span class="post">POST</span><span class="beforePost">/v1/tmp_transactions/create</span>

A Yapay Intermediador fornece uma ferramenta poderosa para sites que não possuem um carrinho de compras e querem oferecer a possibilidade de visitantes escolherem produtos e finalizarem uma compra.


Esta ferramenta exclusiva também permite que seja possível o seu uso em um ambiente multi-vendedor, onde o site/marketplace pode fornecer um carrinho de compras para todas as lojas simultaneamente, fazendo com que o comprador tenha uma experiência única de compra com a Yapay Intermediador.


| Endereço para Integração |                                                                               |
|--------------------------|------------------------------------------------------------------------------|
| Ambiente de Testes       | https://api.intermediador.sandbox.yapay.com.br/v1/tmp_transactions/create   |
| Ambiente de Produção     | https://api.intermediador.yapay.com.br/v1/tmp_transactions/create           |
| Protocolo                | Rest/HTTP                                                                    |

> É necessario utilizar o Protocolo de Criptografia TLS na versão 1.2. 

# Códigos de Exemplo


```javascript
    {
        "token_account": "SEU_TOKEN",
        "postal_code_seller": "17516000",
        "shipping_type": "Sedex",
        "shipping_price": "10",
            
        "transaction_product":[  
            {  
                "description": "Infinity Stone",
                "quantity": "1",
                "price_unit": "1500.00",
                "code": "1"
            }
        ]   
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
                    <description>Infinity Stone</description>
                    <extra nil="true"/>
                    <price_unit type="decimal">1500.0</price_unit>
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

| Código    |  Mensagem                                   |
|-----------|---------------------------------------------|
| 001001	| Token inválido ou não encontrado            |
| 003003	| Forma de Pagamento Inválido                 |
| 003004	| Número da Parcela Inválido                  |
| 003010	| Forma de pagamento inválida                 |
| 003011	| Numero do cartão inválido                   |
| 003012	| Nome do cartão em branco                    |
| 003014	| Código de segurança inválido                |
| 003015	| Mês de vencimento do cartão inválido        |
| 003016	| Número de parcelas inválido                 |
| 003020	| Ano de vencimento do cartão inválido        |
| 003021	| O vendedor não pode ser igual ao comprador  |
| 003022    | Data final inválida                   	  |
| 003023    | Data inicial inválida                       |
| 003029	| Código de segurança inválido                |
| 003039	| Vendedor inválido ou não encontrado         |
| 003065	| Valor menor que mínimo permitido            |
| 009006	| Número da parcela maior que o permitido     |
| 017001    | Token de sessão inválido                    |
| 058001	| Revendedor inválido.                        |
| 060003    | Token de acesso inválido ou expirado.       |


# Tabela de Parâmetros

Para a integração via <span class="post">post</span>, segue abaixo os dados necessários para envio:

| Dados de Entrada                                |	Obrig.  |	Descrição                                |
|-------------------------------------------------|---------|--------------------------------------------|
| token_account                                   |  Sim    | Token da conta                             |
| reseller_token                                  |  Não    | Token do revendedor                        |
| payment_tax_code                                |  Não    | Tabela de Taxa                             |
| token_transaction<sup>1</sup>                   |  Não    | Token da transação temporária já existente |
| order_number                                    |  Não    | Número do pedido                           | 
| sub_store                                       |  Não    | Nome da subloja                            |
| free                                            |  Não    | Campo free                                 |
| price_additional                                |  Não    | Preço adicional                            |
| price_discount                                  |  Não    | Desconto Adicional                         |
| url_notification                                |  Não    | URL de Notificação                         |
| url_success                                     |  Não    |  URL para redirecionamento caso concluída a transação com sucesso <sup>5</sup>   |
| url_process                                     |  Não    |  URL para redirecionamento caso pedido esteja aguardando a confirmação de pagamento <sup>5</sup> |
| url_cancel                                      |  Não    |  URL para redirecionamento caso concluída a transação mas ocorreu falha no pagamento <sup>5</sup> |
| postal_code_seller                              |  Sim    | CEP do Vendedor                            |
| postal_code_customer                            |  Não    | CEP do Cliente                             |
| available_payment_methods                       |  Não    | Meios de Pagamento disponíveis             |
| max_split_transaction                           |  Não    | Quantidade máxima de parcelamento          |
| shipping_type                                   |  Não    | Tipo de Frete                              |
| shipping_price                                  |  Não    | Valor do Frete                             |
| url_notification                                |  Não    | URL de Notificação                         |
| transaction_product[][code]                     |  Sim    | Código do Produto                          |
| transaction_product[][description]              |  Sim    | Descrição do Produto                       |
| transaction_product[][quantity]                 |  Sim    | Quantidade do produto                      |
| transaction_product[][price_unit]               |  Sim    | Valor unitário do Produto                  |
| transaction_product[][weight]<sup>2</sup>       |  Não    | Peso do Produto                            |
| transaction_product[][extra]                    |  Não    | Campo de informação extra                  |
| transaction_product[][url_img]                  |  Não    | URL de Imagem do Produto                   |
| transaction_product[][sku_code]                 |  Não    | Código SKU do Produto                      |
| transaction_product[][type_product]<sup>3</sup> |  Sim    | Tipo do produto                            |
| transaction_product[][edit] <sup>4</sup>        |  Não    | Permite edição do produto?                 |
| affiliates[][reseller_token]                    |  Não    | Token do afiliado                          |
| affiliates[][email]                             |  Não    | E-mail do afiliado                         |
| affiliates[][percentage]                        |  Não    | Percentual do afiliado                     |
| affiliates[][commission_amount]                 |  Não    | Valor fixo do afiliado                     |
| affiliates[][type_affiliate]                    |  Não    | Tipo de afiliado                           |


> <sup>1</sup> Enviando o token_transaction você está atualizando uma transação temporária que já existe.

> <sup>2</sup> Informando o peso do produto você está possibilitando o cálculo do frete dessa transação.

> <sup>3</sup> Tipo de produto deve ser S para Serviço ou vazio para produto normal.

> <sup>4</sup> Nesse campo você informa se é possível realizar a alteração da quantidade do produto no checkout Yapay.  True ou false.

> <sup>5</sup> Para o redirecionamento basta utilizar somente o campo '[url_process]', pois caso seja omitido os campos '[url_success]' e '[url_cancel]', é utilizado o campo '[url_process]' para o redirecionamento.
