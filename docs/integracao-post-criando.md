## Exemplo de código

Abaixo você consegue visualizar o código de exemplo:

| Endereço para Integração |                                                                         |
|--------------------------|------------------------------------------------------------------------|
| Ambiente de Testes       | https://tc.intermediador.sandbox.yapay.com.br/payment/transaction   |
| Ambiente de Produção     | https://tc.intermediador.yapay.com.br/payment/transaction           |


```html
  <form method="post" action="https://tc.intermediador.sandbox.yapay.com.br/payment/transaction"> 
        <!-- Campos obrigatórios --> 
       <input type="hidden" name="token_account" value="SEU_TOKEN_AQUI"> 

      <!-- Dados do produto 1 --> 
       <input type="hidden" name="transaction_product[][description]" value="Notebook Prata"> 
       <input type="hidden" name="transaction_product[][quantity]" value="1"> 
       <input type="hidden" name="transaction_product[][price_unit]" value="2430.00"> 


       <!-- Código de referência do pagamento no seu sistema (opcional) --> 
       <input type="hidden" name="order_number" value="562789"> 

       <!-- submit do form --> 
       <input type="submit" name="submit" value="Pagar com Yapay" > 
  </form>
```

> Note que nas informações acima que alguns dados possuem uma característica diferente, tendo um elemento [] dentro de sua formatação. Isso ocorre justamente para permitir que sejam enviados diversos itens na mesma requisição.

## Tabela de campos

Os dados adicionais que podem ser enviados neste <span class="post">POST</span> são:

| Dados de Entrada                      | Formato / Tam. Max              | Descrição                                |
|---------------------------------------|---------------------------------|------------------------------------------|
| transaction_product[][code]           |  Número / 20                    |  Código do produto                       |
| transaction_product[][extra]          |  Texto / 45                     |  Informações extras do produto           |
| transaction_product[][url_img]        |  Url / 255                      |  URL da imagem do produto                |
| transaction_product[][sku_code]       |  Texto / 20                     |  Código SKU do produto                   |
| order_number                          |  Número / 20                    |  Número do pedido                        |
| free                                  |  Texto / 100                    |  Informações extras da transação         |
| price_additional                      |  Decimal / Ex: 0.00             |  Valor adicional da transação            |
| price_discount                        |  Decimal / Ex: 0.00             |  Valor do desconto da transação          |
| url_notification                      |  Url / 255                      |  Endereço do site de notificação         |
| url_success                           |  Url / 255                      |  URL para redirecionamento caso concluída a transação com sucesso <sup>2</sup>   |
| url_process                           |  Url / 255                      |  URL para redirecionamento caso pedido esteja aguardando a confirmação de pagamento <sup>2</sup> |
| url_cancel                            |  Url / 255                      |  URL para redirecionamento caso concluída a transação mas ocorreu falha no pagamento <sup>2</sup> |
| shipping_type                         |  Texto / 15                     |  Tipo de envio                           |
| shipping_price                        |  Decimal / Ex: 0.00             |  Valor do envio                          |
| sub_store                             |  Texto / 20                     |  Sub-Loja                                |
| url_css                               |  Url / 255                      |  URL do CSS customizado                  |
| available_payment_methods             |  Texto /20                      |  Meios de Pagamento disponíveis          |
| max_split_transaction                 |  Número /10                     |  Número máximo de parcelas               |
| customer[name]                        |  Texto /100                     |  Nome do Comprador                       |
| customer[cpf]                         |  Texto /14                      |  CPF do Comprador                        |
| customer[email]                       |  Texto /100                     |  E-mail do Comprador                     |
| customer[birth_date]                  |  Data / 10                      |  Data de Nascimento do Comprador         |
| customer[contacts][][type_contact]    |  Texto /1                       |  Tipo do Contato.<sup>1</sup> [(Tabela 1)](tabelas.md) |
| customer[contacts][][number_contact]  |  Texto /10                      |  Número do telefone do Comprador         |
| customer[addresses][][type_address]   |  Texto /1                       |  Tipo do Endereço <sup>1</sup> [(Tabela 2)](tabelas.md)           |
| customer[addresses][][postal_code]    |  Texto /8                       |  CEP do endereço do Comprador            |
| customer[addresses][][street]         |  Texto /120                     |  Nome da rua do Comprador                |
| customer[addresses][][number]         |  Texto /10                      |  Número do endereço do Comprador         |
| customer[addresses][][neighborhood]   |  Texto /100                     |  Bairro do endereço do Comprador         |
| customer[addresses][][completion]     |  Texto /100                     |  Complemento do endereço do Comprador    |
| customer[addresses][][city]           |  Texto /120                     |  Cidade do endereço do Comprador         |
| customer[addresses][][state]          |  Texto /2                       |  Estado do endereço do Comprador         |


> <sup>1</sup> Note que nas informações acima que alguns dados possuem uma característica diferente, tendo um elemento [] dentro de sua formatação. Isso ocorre justamente para permitir que sejam enviados diversos itens na mesma requisição.  

> <sup>2</sup> Para o redirecionamento basta utilizar somente o campo '[url_process]', pois caso seja omitido os campos '[url_success]' e '[url_cancel]', é utilizado o campo '[url_process]' para o redirecionamento.
