# Introdução

O Yapay disponibiliza uma versão transparente para a integração de transações, permitindo que o usuário efetue o processamento dos pedidos sem necessitar o redirecionamento para outra aplicação e preenchimento de novos formulários.

![API Transação Yapay](/images/Integracao_api_LV.png "API Transação Yapay")

# Bandeiras e Produtos Suportados

Abaixo você consegue visualizar a tabela com as bandeiras e produtos suportados pelo Yapay Intermediador:


| Bandeira/Produto               | ID Forma de Pagamento | Parcelamento em até | À Vista | Débito |
|--------------------------------|-----------------------|---------------------|---------|--------|
| Visa                           | 3                     | 12                  | Sim     | Não    |
| Mastercard                     | 4                     | 12                  | Sim     | Não    |
| American Express               | 5                     | 12                  | Sim     | Não    |
| Elo                            | 16                    | 12                  | Sim     | Não    |
| Aura                           | 18                    | 12                  | Sim     | Não    |
| Hipercard                      | 20                    | 12                  | Sim     | Não    |
| Hiper                          | 25                    | 12                  | Sim     | Não    |
| JCB                            | 19                    | 1                   | Sim     | Não    |
| Discover                       | 15                    | 1                   | Sim     | Não    |
| Boleto Bancário                | 6                     | 1                   | Sim     | Não    |
| Transf. Online Itaú            | 7                     | 1                   | Sim     | Não    |
| Transf. Online Bradesco        | 22                    | 1                   | Sim     | Não    |
| Transf. Online Banco do Brasil | 23                    | 1                   | Sim     | Não    |
| Peela                          | 14                    | 1                   | Sim     | Não    |
| Pagamento com Saldo            | 8                     | 1                   | Sim     | Não    |


# Fluxo da Transação

De uma forma simplificada, abaixo está disponível o fluxo de status de uma transação dentro do sistema:

![Fluxo de Transação Yapay](/images/status_transacao.png "Fluxo de Transação Yapay")
