# API Cadastrar Cliente

<span class="post">POST</span><span class="beforePost">/v1/people/create</span>

A Yapay permite a criação de contas para auxiliar no processo de integração.

Através da API de Cadastro de Cliente é possível criar clientes do tipo Pessoa Física ou Pessoa Jurídica, onde são retornados os dados do cliente para integração.

| Endereço para Integração |                                                                  |
|--------------------------|------------------------------------------------------------------|
| Ambiente de Testes       | https://api.intermediador.sandbox.yapay.com.br/v1/people/create  |
| Ambiente de Produção     | https://api.intermediador.yapay.com.br/v1/people/create          |
| Protocolo                | Rest/HTTP                                                        |


# Códigos de Exemplo


```javascript
    {    
        "account_type": "1",
        "email": "stephen.strange@avengers.com",
        "name": "Stephen Strange",
        "cpf": "17786724699",
        "birth_date": "21/12/1985",
        "relationship": "S",
        "gender": "M",
        "type_address": "B",
        "street": "Av Paulista",
        "number": "3",
        "completion": "111",
        "neighborhood": "Jd Paulista",
        "postal_code": "17516000",
        "city": "São Paulo",
        "state": "SP",      
            "contacts":[  
                 {  
                    "type_contact":"H",
                    "number_contact":"1133221122"
                 }       
            ],
        "type_response": "J"
    }
```


# Resposta da API

> Exemplo de resposta em JSON com `sucesso` baseando no envio do exemplo:

```javascript
    {
        "message_response": {
            "message": "success"
        },
        "data_response": {
            "session_id": "70411817e3b35a21f8d47b998f18k",
            "token_account": "3ggs3c002d2d2db",
            "customer_name": "Stephen Strange",
            "customer_address_id": 160208,
            "email": "stephen.strange@avengers.com"
        }
    }
```


> Exemplo de resposta com `erro` baseando no envio do exemplo:


```javascript
    {
        "message_response": {
            "message": "error"
        },
        "error_response": {
            "validation_errors": [
                {
                    "code": "6",
                    "message": "já está em uso",
                    "field": "cpf",
                    "message_complete": "CPF já está em uso"
                }
            ]
        }
    }
```


As mensagens de erros retornados pela API estão listadas na tabela abaixo:

| Código    | Mensagem                |
|-----------|-------------------------|
|  036004   | Cliente não encontrado  |
|  036010   | Tipo de Conta inválido  |
|  058001   | Revendedor inválido.    |



# Tabela de Parâmetros

Para a integração via <span class="post">POST</span>, segue abaixo os dados necessários para envio:

| Dados de Entrada           |  Obrig.         | Formato / Tam. Max   | Descrição                      |
|----------------------------|-----------------|----------------------|--------------------------------|
| account_type               | Sim             | Número               | Tipo de Conta                  |
| trade_name                 | Sim<sup>2</sup> | Texto                | Nome Fantasia                  |
| company_name               | Sim<sup>2</sup> | Texto                | Razão Social                   |
| cnpj                       | Sim<sup>2</sup> | Texto                | CNPJ                           |
| url                        | Não             | Texto                | Url da Empresa                 |
| url_notification           | Não             | Texto                | Url de Notificação             |
| inscricao_municipal        | Não             | Texto                | Inscrição Municipal            |
| url_css                    | Não             | Texto                | Configuração da URL CSS        |
| email                      | Sim             | Texto                | E-mail                         |
| name                       | Sim             | Texto                | Nome Completo                  |
| birth_date                 | Não             | Data                 | Data de Aniversário            |
| cpf                        | Sim             | Texto                | CPF                            |
| relationship               | Não             | Texto                | Estado Civil                   |
| gender                     | Não             | Texto                | Sexo (Tabela 3)                |
| contacts[][type_contact]   | Sim             | Texto                | Tipo de Contato                |
| contacts[][number_contact] | Sim             | Texto                | Número de telefone<sup>1</sup> |
| type_address               | Sim             | Texto                | Tipo de endereço               |
| street                     | Sim             | Texto                | Logradouro                     |
| number                     | Sim             | Texto                | Número                         |
| neighborhood               | Sim             | Texto                | Bairro                         |
| completion                 | Não             | Texto                | Complemento                    |
| postal_code                | Sim             | Texto                | CEP                            |
| city                       | Sim             | Texto                | Cidade                         |
| state                      | Sim             | Texto                | Estado                         |
| payment_tax_code           | Não             | Número               | Código Tabela de Taxas         |
| reseller_token             | Não             | Texto                | Token do Revendedor            |
| password                   | Não             | Texto                | Senha do cliente para acessar o painel |
| type_response              | Não             | Texto                | J = JSON  / Outros = XML        |


> <sup>1</sup> Note que nas informações acima que alguns dados possuem uma característica diferente, tendo um elemento [] dentro de sua formatação. Isso ocorre justamente para permitir que sejam enviados diversos itens na mesma requisição.

> <sup>2</sup> Campos obrigatórios para cadastros de pessoa jurídica.
