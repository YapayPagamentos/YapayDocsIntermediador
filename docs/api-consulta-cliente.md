# API Consultar Cliente


<span class="post">POST</span><span class="beforePost">/v1/people/get_person_by_cpf_and_email</span>

A Yapay permite a consulta de contas para auxiliar no processo de integração.

Através da API de Consulta de Cliente é possível criar clientes do tipo Pessoa Física ou Pessoa Jurídica, onde são retornados os dados do cliente para integração.

| Endereço para Integração |                                                                         |
|--------------------------|------------------------------------------------------------------------|
| Ambiente de Testes       | https://api.intermediador.sandbox.yapay.com.br/v1/people/get_person_by_cpf_and_email  |
| Ambiente de Produção     | https://api.intermediador.yapay.com.br/v1/people/get_person_by_cpf_and_email           |
| Protocolo                | Rest/HTTP                                                              |

> É necessario utilizar o Protocolo de Criptografia TLS na versão 1.2. 

# Códigos de Exemplo


```javascript
    {
      "email": "dianaprince@amazonas.br"
    }
```


# Resposta da API

> Exemplo de resposta em XML com `sucesso` baseando no envio do exemplo:

```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <people>
        <data_response>
            <name>Tony Stak</name>
            <cpf>333.XXX.X18-XX</cpf>
            <email>tony@stak.com</email>
            <has_card type="boolean">true</has_card>
            <company nil="true"/>
        </data_response>
        <message_response>
            <message>success</message>
        </message_response>
    </people>
```


> Exemplo de resposta com `erro` baseando no envio do exemplo:


```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <people>
        <error_response>
            <errors type="array">
                <error>
                    <message>Cliente não encontrado</message>
                    <code>036004</code>
                </error>
            </errors>
        </error_response>
        <message_response>
            <message>error</message>
        </message_response>
    </people>
```


As mensagens de erros retornados pela API estão listadas na tabela abaixo:

| Código    | Mensagem                |
|-----------|-------------------------|
|  036004   | Cliente não encontrado  |



# Tabela de Parâmetros

Para a integração via <span class="post">POST</span>, segue abaixo os dados necessários para envio:

| Dados de Entrada           |  Obrig.         | Formato / Tam. Max   | Descrição                      |
|----------------------------|-----------------|----------------------|--------------------------------|
| cpf                        | Sim             | Texto                | CPF<sup>1</sup>                |
| email                      | Sim             | Texto                | E-mail<sup>1</sup>             |

> <sup>1</sup> Um dos parâmetros é obrigatório, `cpf` ou o `email`.
