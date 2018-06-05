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

| Código    |  Mensagem                                        |
|-----------|--------------------------------------------------|
|  001001   |     Token inválido ou não encontrado             |
|  003003   |     Forma de Pagamento Inválido                  |
|  003004   |     Número da Parcela Inválido                   |
|  003010   |     Forma de pagamento inválida                  |
|  003011   |     Numero do cartão inválido                    |
|  003012   |     Nome do cartão em branco                     |
|  003014   |     Código de segurança inválido                 |
|  003015   |     Mês de vencimento do cartão inválido         |
|  003016   |     Número de parcelas inválido                  |
|  003020   |     Ano de vencimento do cartão inválido         |
|  003021   |     O vendedor não pode ser igual ao comprador   |
|  003029   |     Código de segurança inválido                 |
|  003039   |     Vendedor inválido ou não encontrado          |
|  003065   |     Valor menor que mínimo permitido             |
|  009006   |     Número da parcela maior que o permitido      |
|  058001   |     Revendedor inválido.                         |