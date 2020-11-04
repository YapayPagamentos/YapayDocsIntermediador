## Boas Práticas de Integração

Nesse artigo será possível verificar algumas dicas para integração com a nossa [API de Transação](https://intermediador.dev.yapay.com.br/#/transacao-introducao). É importante seguir este artigo e validar antes de enviar as transações para análise dos parâmetros de criação para o email [integracao@yapay.com.br](mailto:integracao@yapay.com.br).


## Recomendações de validações de envio de parâmetros

Para criar uma transação nós precisamos de alguns campos obrigatórios, esses campos devem ser validados antes de enviar para a API assim é possível evitar retornos de erros. Abaixo as validações recomendadas para cada campo.


> **Parâmetros de dados do cliente**

**customer[cpf]** Deve ser enviado o número de CPF válido. Apenas números.

**customer[cnpj]** Deve ser enviado o número de CNPJ válido. Apenas números.

**customer[email]** O e-mail deve ser válido, respeitando regras .com .com.br e @gmai, @hotmai, @teste **não** são aceitos.

**customer[birth_date]** Deve ser enviado como string no formato DD/MM/YYYY.

**customer[contacts][][type_contact]** O tipo de contato deve ser H-Residencial, M-Celular ou W-Comercial. De acordo com a quantidade de caracteres enviado **contacts[number_contact]**.

**customer[contacts][][number_contact]** O número do telefone deve ser validado a quantidade de caracteres máximo 15 e minimo 8.

**customer[addresses][][postal_code]** Deve ser enviado em TEXTO e no máximo 8 caracteres. 

**customer[addresses][][street]** Deve ser enviado apenas a RUA, e enviando o número no parâmetro **customer[addresses][][number]**.

**customer[addresses][][state]** Deve ser enviado a sigla do estado. Exemplo: SP


> **Parâmetro IP**

**transaction[customer_ip]** Deve ser enviado o IP do devide. Normalmente enviado pelo REMOTE_ADDR.


> **Parâmetro Número do Pedido**

**transaction[order_number]** Máximo 20 caracteres. Caso não seja enviado esse parâmetro será o mesmo que o ID da Transação. **O NÚMERO DO PEDIDO NÃO DEVE SE REPETIR**


> **Parâmetros valores**

**transaction[price_discount]** Caso tenha casas decimais, deve ser validado para enviar com duas casas decimais.

**transaction[shipping_price]** Caso tenha casas decimais, deve ser validado para enviar com duas casas decimais.

**transaction[price_additional]** Caso tenha casas decimais, deve ser validado para enviar com duas casas decimais.


> **Parâmetros do produto**

**transaction_product[][sku_code]** Máximo 50 caracteres.

**transaction_product[][price_unit]** Caso tenha casas decimais, deve ser validado para enviar com duas casas decimais.


> **Parâmetro finger_print**

O parâmetro `finger_print` é de extrema importância nas transações de cartão de crédito, deve ser enviado em TODAS as transações que sejam cartão. Veja como implementa-lo clicando [aqui](https://intermediador.dev.yapay.com.br/#/transacao-fingerprint).


> **Parâmetros de Pagamento**

**payment[payment_method_id]** Deve ser verificada a tabela [Formas de Pagamentos](https://intermediador.dev.yapay.com.br/#/tabelas?id=tabela-3-formas-de-pagamento) aceitas pela Yapay.

**payment[split]** Algumas formas de pagamento não aceitam parcelamento, apenas à vista, deve ser validado se o payment[payment_method_id] for igual a 5 ou 19 e apenas apresentar uma parcela.


> **Parâmetros de Boleto**

**payment[billet_date_expiration]** Deve ser enviado no formato DD/MM/YYYY.


> **Parâmetros de Cartão de Crédito**

**payment[card_token]** Quando é utilizada a API de Cadastro de Cartão de Crédito é retornado o `card_token`, que deve ser enviado na API de Transação juntamente com o parâmetro `payment[card_cvv]`. Nós não armazenamos o parãmetro `card_cvv` devido as regras do PCI-DSS. Recomendamos que seja salvo em sua aplicação os parãmetros `card_token` e `card_cvv` ou salvar apenas o `card_cvv` e deverá solicitar o `card_cvv` em TODAS as transações. **IMPORTANTE SEMPRE ENVIAR OS DOIS PARÂMETROS JUNTOS, pois se não for enviado as transações serão recusadas pela adquirente.**

**payment[card_name]** Não deve ser enviado números nesse parâmetro, validar o input para não aceitar que seja digitado números.

**payment[card_number]** Não deve ser enviado letras nesse parâmetro, validar o input para não aceitar que seja digitado letras.

**payment[card_expdate_month]** O mês de vencimento do cartão de crédito deve ser validado para ser IGUAL ou MAIOR que o mês atual. Deve ser enviado o mês com dois digitos. Exemplo 04

**payment[card_expdate_year]** O ano de vencimento do cartão de crédito deve ser validado para ser IGUAL ou MAIOR que o ano atual. Deve ser enviado o ano com quatro digitos. Exemplo 2022

**payment[card_cvv]** **OBRIGATÓRIO**. Deve ser validado para acertar no máximo 4 caracteres.


> **Parâmetros de Afiliados**

**affiliates[][account_email]** Para melhor fluxo, o e-mail do afiliado deve estar cadastrado na Yapay. 

**affiliates[][percentage]** Deve ser enviado porcentagem de 1-100.

**affiliates[][commission_amount]** Caso tenha casas decimais, deve ser validado para enviar com duas casas decimais.
