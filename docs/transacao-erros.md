# Mensagens de Erros

No caso de erro, a API retorna uma mensagem de erro. Assim é possível identificar o erro ocorrido e realizar o tratamento através do código e/ou mensagem retornada.

Abaixo segue os detalhes de cada nó do JSON de resposta:


```javascript
{
    "message_response": {
        "message": "error"
    },
    "error_response": {
        "general_errors": [
            {
                "code": "003039",
                "message": "Vendedor inválido ou não encontrado"
            }
        ]
    }
}
```


As mensagens de erros retornados pela API estão listadas na tabela abaixo:

| Código    |  Mensagem                                        | Solução                                               |
|-----------|--------------------------------------------------|-------------------------------------------------------|
|  001001   |     Token inválido ou não encontrado             | Verificar o `token_account`                             |
|  003003   |     Forma de Pagamento Inválido                  | Verificar o parâmetro `transaction[payment_method_id]`  |
|  003004   |     Número da Parcela Inválido                   | Verificar o parâmetro `transaction[split]`              |
|  003011   |     Numero do cartão inválido                    | Verificar o parâmetro `transaction[card_number]`        |
|  003012   |     Nome do cartão em branco                     | Verificar o parâmetro `transaction[card_name]`          |
|  003014   |     Código de segurança inválido                 | Verificar o parâmetro `transaction[card_cvv]`                |
|  003015   |     Mês de vencimento do cartão inválido         | Verificar o parâmetro `transaction[card_expdate_month]` |
|  003020   |     Ano de vencimento do cartão inválido         | Verificar o parâmetro `transaction[card_expdate_year]`  |
|  003021   |     O vendedor não pode ser igual ao comprador   | Verificar os parâmetros token_account, `costumer[email]` e `costumer[cpf]`. Os dados não podem ser iguais |
|  003039   |     Vendedor inválido ou não encontrado          | Verificar o `token_account` |
|  003065   |     Valor menor que mínimo permitido             | Verificar os transaction[split] e (`transaction_product[price_unit]` x `transaction_product[quantity]`). Somando os valores transaction[shipping_price] + (`transaction_product[price_unit]` x `transaction_product[quantity]`) o valor mínimo da parcela deve ser R$ 10,00 |
|  009006   |     Número da parcela maior que o permitido      | Verificar os parâmetros `transaction[payment_method_id]` e `transaction[split]` se a quantidade de parcelas é aceita pelo Meio de Pagamento. <sup>1</sup> |
|  058001   |     Revendedor inválido.                         | Verifique o parâmetro `reseller_token`. Deve estar devidamente configurado na Yapay como Revendedor |
|  037010   |     E-mail do afiliado informado deve ser diferente do vendedor                         | O email enviado como cliente não pode ser o mesmo que o e-mail do vendedor (token_account) |
|  3   |     Comissão Valor da comissão é maior que o valor do pedido                         | O valor da comissão está sendo enviado maior que o valor da comissão do afiliado. |
|  037022   |     Afiliado não possui conta. Email: email_informado                         | O e-mail enviado no parâmetro `affiliates[account_email]` não tem cadastro na Yapay. TODAS as contas de afiliados devem ter conta cadastrada. |


> <sup>1</sup> <a href="/#/transacao-introducao?id=bandeiras-e-produtos-suportados">Clique Aqui</a> e verifique pela nossa tabela de Produtos e Bandeiras Suportadas


Os erros de validações de parâmetros serão retornados STATUS CODE `422 - Unprocessable Entity`. Exemplo:

```javascript
{
    "message_response": {
        "message": "error"
    },
    "error_response": {
        "validation_errors": [
            {
                "code": "3",
                "message": "não é válido",
                "field": "price_discount",
                "message_complete": "Valor Desconto não é válido"
            }
        ]
    },
    "additional_data": {
        "transaction_id": null,
        "order_number": null,
        "status_id": null,
        "status_name": null,
        "token_transaction": null
    }
}
```
