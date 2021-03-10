Na integração existem alguns campos com informações pré-definidas, onde deverão ser enviadas conforme o padrão existente, se for necessário enviar o campo na requisição, ou poderá tratar a informação conforme retorno recebido.

Abaixo segue tabelas com essas informações pré-definidas:

## ** Tabela 1 - Contato**


| Contato |   |
|--------------------|---|
| Residencial        | H |
| Celular            | M |
| Comercial          | W |


## **Tabela 2 - Tipos de Endereço**


| Tipos de Endereço | |
|-------------|---|
| Cobrança    | B |
| Entrega     | D |


## **Tabela 3 - Formas de Pagamento**

| **Transferências Online**       | ID |
|---------------------------------|---:|
| Itaú Shopline                   | 7  |
| Transf. Online Bradesco         | 22 |
| Transf. Online Banco do Brasil  | 23 |


| **Boleto**       |  ID  |
|---------------------------------|---:|
| **Boleto Bancário**             | 6  |

| **Saldo**       |  ID  |
|---------------------------------|---:|
| **Pagamento com Saldo**         | 8  |



| **Cartões de Crédito**          |  ID  | Credito Parcelado |
|---------------------------------|----:|-----:|
| Visa                            | 3  | 12x |
| Mastercard                      | 4  | 12x |
| American Express                | 5  | 12x |
| Discover                        | 15 | À Vista |
| Elo                             | 16 | 12x |
| Aura                            | 18 | 12x |
| JCB                             | 19 | À Vista |
| Hipercard                       | 20 | 12x |
| Hiper (Itaú)                    | 25 | 12x |


## **Tabela 4 - Status da Transação**

| Status da Transação em Portugês   | Status da Transação em Inglês  | Status ID  |
|---------------------------------|----------------------------------|-----------:|
| Aguardando Pagamento            | waiting_payment                  | 4  |
| Aprovada                        | approved                         | 6  |
| Cancelada                       | canceled                         | 7  |
| Em Contestação                  | contestation                     | 24 |
| Em Contestação                  | chargeback                       | 24 |
| Em Monitoramento                | monitoring                       | 87 |
| Reprovada                       | failed                           | 89 |


## **Tabela 5 - Gênero**

| Gênero    | |
|-----------|---:|
| Masculino | M |
| Feminino  | F |


## **Tabela 6 - Estado Civil**

| Estado Civil | |
|------------|---:|
| Solteiro   | S |
| Casado     | M |
| Separado   | A |
| Divorciado | D |
| Viúvo      | W |


## **Tabela 7 - Status da Conta**

| Status da Conta | |
|----------|-----:|
| Ativo    | 2   |
| Inativo  | 3   |
| Suspeito | 114 |


## **Tabela 8 - Tipo de Conta**

| Tipo de Conta | |
|--------------|-----:|
| Pessoal      | 1   |
| Empresarial  | 2   |

