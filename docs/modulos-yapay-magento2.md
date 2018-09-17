## Módulo Magento 2 - Yapay

Módulo de pagamento para o Magento 2, cuja a finalidade é fornecer com a integração da plataforma Yapay.

### Formas de pagamento integradas

- [x] Boleto Bancário
- [x] Cartões de crédito
- [x] Transferência Bancário


### Versões que o Módulo pode ser Instalado

- [x] 2.0.x
- [x] 2.1.x
- [x] 2.2.x

# Instalação do Módulo Yapay

- Realize o download do módulo, clicando em **clone or download** após isso clique em **Download ZIP** e siga os seguintes passos
de acordo com a forma que sua loja foi instalada:

### Loja instalada por meio do composer

-  Se sua loja foi criada usando o gerenciador de dependência composer, realize os seguintes passos

1. Crie o diretório **code** dentro de **app**
2. Extraia o conteúdo do download ZIP para dentro da pasta **code**
3. Verifique se está dessa maneira seus diretórios na sua loja **_app/code/Yapay/Magento2_**
4. Execute o comando **_bin/magento setup:upgrade_**
5. Execute o comando **_bin/magento setup:di:compile_**
6. Execute o comando **_bin/magento setup:static-content:deploy -f_**

### Loja instalada por meio do github

- Caso sua loja tenha sido criada por meio do clone ou download do projeto magento disponibilizada no github do Magento2, realize os seguintes passos.

1. Extraia o conteúdo do download ZIP para dentro da pasta **code**
2. Verifique se está dessa maneira seus diretórios na sua loja **_app/code/Yapay/Magento2_**
3. Execute o comando **_bin/magento setup:upgrade_**
4. Execute o comando **_bin/magento setup:di:compile_**
5. Execute o comando **_bin/magento setup:static-content:deploy -f_**

### Clonando o módulo do Yapay

- Caso possua o **git** instalado pode pular os passos de download do módulo apenas realizando o *clone* do módulo para dentro do diretório **code**




