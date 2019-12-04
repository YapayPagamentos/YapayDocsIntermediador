# API de Simulação de Parcelamento



<span class="post">POST</span><span class="beforePost">/api/v1/transactions/simulate_splitting</span>

A Yapay disponibiliza a API de Simulação de Cálculo de Parcelamento para facilitar o calculo de parcelamento, onde através do token do lojista e o valor da transação, é retornada a simulação do parcelamento de todas as formas de pagamento.

A API de Simulação de Cálculo de Parcelamento é utilizada somente para facilitar a exibição deste parcelamento na loja virtual, onde é enviada somente a quantidade de parcelas para a <a href="/#/transacao-introducao" target="_blank" class="linkPadraoVerde">API de Transação</a>.

| Endereço para Integração |                                                                                   |
|--------------------------|-----------------------------------------------------------------------------------|
| Ambiente de Testes       | https://api.intermediador.sandbox.yapay.com.br/v1/transactions/simulate_splitting |
| Ambiente de Produção     | https://api.intermediador.yapay.com.br/v1/transactions/simulate_splitting         |
| Protocolo                | Rest/HTTP                                                                         |

> É necessario utilizar o Protocolo de Criptografia TLS na versão 1.2. 

# Códigos de Exemplo


```javascript
    {  
       "token_account":"SEU_TOKEN",
       "price":"1000"
    }
```


# Resposta da API

> Exemplo de resposta em XML com `sucesso` baseando no envio do exemplo:

```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <transaction>
        <data_response>
            <payment_methods type="array">
                <payment_method>
                    <splittings type="array">
                        <splitting>
                            <split type="integer">1</split>
                            <value_split>1134.30</value_split>
                            <value_transaction>1134.30</value_transaction>
                            <addition_retention>0.00</addition_retention>
                            <split_rate type="integer">0</split_rate>
                        </splitting>
                        <splitting>
                            <split type="integer">2</split>
                            <value_split>584.14</value_split>
                            <value_transaction>1168.28</value_transaction>
                            <addition_retention>0.00</addition_retention>
                            <split_rate type="decimal">1.99</split_rate>
                        </splitting>                    
                    </splittings>
                    <price_customer>1134.30</price_customer>
                    <price_seller>1061.42</price_seller>
                    <price_original>1134.30</price_original>
                    <split type="integer">12</split>
                    <payment_method_name>Visa</payment_method_name>
                    <payment_method_id type="integer">3</payment_method_id>
                </payment_method>
                <payment_method>
                    <splittings type="array">
                        <splitting>
                            <split type="integer">1</split>
                            <value_split>1134.30</value_split>
                            <value_transaction>1134.30</value_transaction>
                            <addition_retention>0.00</addition_retention>
                            <split_rate type="integer">0</split_rate>
                        </splitting>
                        <splitting>
                            <split type="integer">2</split>
                            <value_split>584.14</value_split>
                            <value_transaction>1168.28</value_transaction>
                            <addition_retention>0.00</addition_retention>
                            <split_rate type="decimal">1.99</split_rate>
                        </splitting>                    
                    </splittings>
                    <price_customer>1134.30</price_customer>
                    <price_seller>1061.42</price_seller>
                    <price_original>1134.30</price_original>
                    <split type="integer">12</split>
                    <payment_method_name>Mastercard</payment_method_name>
                    <payment_method_id type="integer">4</payment_method_id>
                </payment_method>
                <payment_method>
                    <splittings type="array">
                        <splitting>
                            <split type="integer">1</split>
                            <value_split>1134.30</value_split>
                            <value_transaction>1134.30</value_transaction>
                            <addition_retention>0.00</addition_retention>
                            <split_rate type="integer">0</split_rate>
                        </splitting>
                    </splittings>
                    <price_customer>1134.30</price_customer>
                    <price_seller>1061.42</price_seller>
                    <price_original>1134.30</price_original>
                    <split type="integer">1</split>
                    <payment_method_name>Boleto Bancario</payment_method_name>
                    <payment_method_id type="integer">6</payment_method_id>
                </payment_method>
        </data_response>
        <message_response>
            <message>success</message>
        </message_response>
    </transaction>
```


> Exemplo de resposta com `erro` baseando no envio do exemplo:


```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <transaction>
        <error_response>
            <errors type="array">
                <error>
                    <code>001001</code>
                    <message>Token inválido ou não encontrado</message>
                </error>
            </errors>
        </error_response>
        <message_response>
            <message>error</message>
        </message_response>
    </transaction>
```


As mensagens de erros retornados pela API estão listadas na tabela abaixo:

| Código   |  Mensagem                                    | 
|----------|----------------------------------------------|
|  001001  | Token inválido ou não encontrado             |
|  003002  | Valor da Transação Inválido                  |
|  003010  | Forma de pagamento inválida                  |
|  003004  | Número da Parcela Inválido                   |
|  009006  | Número da parcela maior que o permitido      |
|  009003  | Tabela taxa inativa ou não encontrada        |


# Tabela de Parâmetros

Para a integração via <span class="post">POST</span>, segue abaixo os dados necessários para envio:

| Dados de Entrada                       |  Obrig.  | Formato / Tam. Max   | Descrição                     |
|----------------------------------------|----------|----------------------|-------------------------------|
| token_account                          |   Sim    |  Texto / 20          |  Token da conta da Loja       |   
| price                                  |   Sim    |  Decimal / 11        |  Valor da Transação           |  
| type_response                          |   Não    |  Texto / 20          |  Tipo de Resposta (J => JSON, OUTROS => XML)           |  
