# PrestaShop


Para disponibilizar a Yapay como facilitador de pagamento na plataforma PrestaShop, basta baixar o pacote disponível no site institucional da Yapay, extrair a pasta com o módulo, copiar para o diretório padrão e configurar o módulo.

Fique atento que sua versão de instalação, a plataforma Prestashop deve ser compatível com o módulo Yapay.

> Nosso módulo do PrestaShop está disponível apenas até a versão 1.6

> 1- Instalação do Módulo Prestashop


Para instalar módulo é necessário baixar o pacote do PrestaShop:

<a href="https://intermediador.dev.yapay.com.br/download/yapay/prestashop/yapay_prestashop2.5.zip" class="btn  btn-default btn-wide btn-call-to-action btnMagento"><i class="fa fa-arrow-circle-down" aria-hidden="true"></i>PrestaShop</a>

Descompacte o arquivo baixado e copie a pasta para o diretório de módulos da sua instalação PrestaShop.

Passos para instalação via FTP, utilizando o Filezilla:

1. Enviar a pasta extraída para o servidor da loja virtual, utilizando um software FTP (neste exemplo utilizamos o Filezilla)

2. Ao efetuar a conexão no FTP, no lado direito serão mostradas as pastas que estão dentro do servidor, acesse a pasta do prestashop

3. Dentro da pasta do PrestaShop existe um diretório chamado **“Modules”**, local onde devem ser instalados todos os arquivos do módulo, entrar na pasta **“Modules”** e enviar a pasta que extraída da Yapay

Cuidado para não arrastar em cima de uma pasta, se isso acontecer você terá uma pasta dentro da outra e então este módulo não funcionará.

![PrestaShop, instalação](/images/prestashop/install_prestashop_1.png "PrestaShop, instalação")

Após a conclusão do envio do módulo Yapay, acessar a administração do PrestaShop e entrar na seção de **“Módulos”**.

Na opção de busca, digitar Yapay e selecionar o módulo que já deverá estar listado na consulta:

![PrestaShop, instalação](/images/prestashop/install_prestashop_2.png "PrestaShop, instalação")

Será mostrado o módulo conforme a imagem abaixo. Clicar no botão install ou instalar (caso sua loja já esteja traduzida) no lado direito da listagem:

![PrestaShop, instalação](/images/prestashop/install_prestashop_3.png "PrestaShop, instalação")

Será necessário inserir dados de cadastro de sua conta para liberar os pagamentos em sua conta Yapay.

> 2- Configuração do Módulo PrestaShop


Na página de módulos, clique em **Configure (Configuração)** para acessar o módulo Yapay.

Será carregada a página do módulo com as opções de configuração abaixo:

![PrestaShop, instalação](/images/prestashop/install_prestashop_4.png "PrestaShop, instalação")


> Opções de configuração Tray Checkout:


**Token:** campo obrigatório gerado no painel de administração Yapay

**URL de notificação de status:** URL utilizada pelo Yapay para alterar os status dos pedidos

**Prefixo do Pedido:** campo opcional, utilizado para concatenar com o número do pedido da loja ao integrar com a Tray

**Ambiente de Teste (Sandbox):** ambiente utilizado pela loja para realizar testes de integração com o Yapay – muita atenção para não manter este ambiente habilitado quando a loja estiver efetivamente vendendo

**Ativar Yapay via Redirect:** existem duas opções de carregamento do Yapay, opção de modal que carrega o Yapay sem sair da loja e Redirect que redireciona o cliente para realizar o pagamento na página do Yapay e retorna na finalização

**Atenção:** Após salvar as configurações, caso o módulo não fique disponível, será necessário alterar as configurações de cache.

