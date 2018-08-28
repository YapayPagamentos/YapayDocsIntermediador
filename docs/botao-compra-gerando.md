# Gerando Botão de Compra

Você vende um único produto? Quer fazer alguma venda em seu site ou blog? Utilize o botão comprar para receber os pagamentos. 

É muito simples. Basta você gerar o código abaixo, copiar o código e colar no seu site.

<div id="page-developers" class="single-page">
<div id="block-buttons" class="block-content text-center bg-green block-content">
    <div class="container">
        <div id="form-content-button" class="form-traycheckout text-left clearfix center col-sm-6">
            <div class="col-sm-12 row">
                <form id="form-generate-button" class="form-tc " action="" method="post">
                    <fieldset class="block-person form-block-content col-sm-12 row">
                        <div class="form-group col-sm-12 ">
                            <label class="form-label" for="generator_token_account">Token de Conta:</label>
                            <input id="generator_token_account" class="form-control input-wide" name="generator_token_account" type="text" value="" placeholder="" required minlength="5" style="width: 250px;">
                        </div>
                        <div class="form-group col-sm-12 ">
                            <label class="form-label" for="generator_product_description">Nome Produto:</label>
                            <input id="generator_product_description" class="form-control input-wide" name="generator_product_description" type="text" value="" required style="width: 350px;">
                        </div>
                        <div class="form-group col-sm-12 ">
                            <label class="form-label" for="generator-product-price">Valor Produto:</label>
                            <input id="generator-product-price" class="form-control input-wide" name="generator-product-price" size="10" type="text" value="" data-thousands="." data-decimal="," data-prefix="R$ " required>
                        </div>
                        <div class="col-sm-12 text-center">
                            <input id="create_button" class="btn btn-default btn-hg btnForm" type="submit" value="Gerar Botão">
                        </div>
                    </fieldset>
                </form>
            </div>
            <div id="block-result" class="col-sm-12" style="display:none">
                <span class="title-result">Copie e cole esse código:</span>
                <div class="button-result text-left codigoBtn">
                    <pre><code class="xml hljs" id="result-button"></code></pre>
                </div>
            </div>
        </div>         
    </div>
    <div class="divider-bottom-line-green"></div>
</div>
</div>

<script>
    hljs.configure({tabReplace: '    '});
    hljs.initHighlightingOnLoad();

    jQuery('#generator-product-price').maskMoney();

    jQuery( "#form-generate-button" ).on('submit', function( event ) {
        event.preventDefault();
        var content = '<form id="form_pagamento" name="form_pagamento" method="post" target="blank" action="https://tc.intermediador.yapay.com.br/payment/transaction"> <input type="hidden" name="token_account" id="token_account" value="{TOKEN_ACCOUNT}"> <input type="hidden" name="transaction_product[][description]" id="product_description" value="{PRODUCT_DESCRIPTION}"> <input type="hidden" name="transaction_product[][quantity]" id="product_quantity" value="1"> <input type="hidden" name="transaction_product[][price_unit]" id="product_price" value="{PRODUCT_PRICE}"> <input type="hidden" name="transaction_product[][extra]" id="product_extra" value=""> <input type="image" src="https://intermediador.dev.yapay.com.br/images/btncomprar.png" value="Comprar" alt="Comprar" border="0"> </form>';
        var token = jQuery('#generator_token_account').val().trim();
        var product = jQuery('#generator_product_description').val().trim();
        var price = jQuery('#generator-product-price').val().replace('R$','').replace('.', '').replace(',', '.').trim();

        if( ( !empty(token) && token.length >= 5 )  && !empty(product) && !empty(price) ){
            var c = content.replace('{TOKEN_ACCOUNT}', token)
                .replace('{PRODUCT_DESCRIPTION}', product)
                .replace('{PRODUCT_PRICE}', price)
                .replace(/[u00A0-u9999<>&]/gim, function(i) { return '&#'+i.charCodeAt(0)+';'; });

            jQuery('#result-button').html( c );

            jQuery('pre code, .code').each(function(i, block) {
                hljs.highlightBlock(block);
            });

            jQuery('#block-result').fadeIn();
        }
    });
</script>
