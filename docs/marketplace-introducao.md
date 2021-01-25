# Introdução

A Yapay disponibiliza a integração transparente com Marketplace, onde o usuário consegue finalizar a compra dentro Marketplace, sem necessitar de redirecionamento para outra aplicação e preenchar novos formulários. O usuário finaliza a compra, e os dados da transação são enviados via API para a Yapay, após a conclusão é enviado um comprovante de compra para o usuário:

> **Observação: a conta do afiliado deve ser criada antes da criação da transação.**

![API Transação Yapay](/images/Integracao_api_LV.png "Marketplace Yapay")

A verificação do cadastro do cliente é feita por uma consulta do CPF do cliente, caso não exista uma conta, o sistema irá criar uma nova conta com os dados que forem submetidos na integração.

Para realizar a integração de forma correta, é necessário incluir um script após o processamento da transação, e também incluir a chamada do plugin no final da página.

> **Para esta integração, deverá ser feito uso da API de Transação, clique [aqui](https://intermediador.dev.yapay.com.br/#/api-consultar-transacao) e veja a documentação.**

> **Para facilitar a exibição do parcelamento no Marketplace, veja a documentação da API de [Simulação de Parcelamento](https://intermediador.dev.yapay.com.br/#/api-simulacao-parcelamento).**
