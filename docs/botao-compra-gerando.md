# Gerando Botão de Compra


<body>
    <head>

    <style type="text/css">

        #page-developers span {
            font-size: 10px;
            line-height: 18px;
            @media (max-width: $mobile-break and 1000px) { 
                font-size: 9px;
            }
        }

        #page-developers  a {
            color: #293272;
        }
        

        #page-developers #form-content-button{
                position: relative;
                background-color: #fff;
                border-radius: 6px;
                border: 1px solid #293272;
                list-style-type: none;
                font-size: 15px;
                line-height: 21px;
                padding: 35px 20px;

            @media (max-width: $mobile-break) {
                font-size: 10px;            
            }   

            @media (max-width: 1091px) {
                font-size: 10px;            
                width: 380px;
            }   

            @media (max-width: 949px) {
                font-size: 10px;            
                width: 300px;
            }           
        }
        
        .form-control {
            border-radius: 0px;

            &:focus {
                outline: none;
                border-color: #293272;
                border-left: 10px solid #293272;
                padding-left: 10px;
                transition: all 0.4s ease; 
            }           

        }   
        
        #page-developers .btnForm {
            font-size: 15px;
            line-height: 21px;
            padding: 10px 65px;
            color: #FFF;
            background-color: #293272;
            outline: none;
            // border-radius: 6px;
            border-radius: 0px;
            border-top-left-radius: 10px;


            @media (max-width: $mobile-break and 1000px) {
                padding: 5px 35px;
                font-size: 12px;
                line-height: 18px;
            }
        }

        #page-developers .btnForm:hover {
            background-color: #FFF;
            border: 1px solid #293272;
            color: #293272;
            transition: all 0.3s ease;      
        }
        
        #page-developers .hljs, #page-help-center .hljs {
            font-size: 10px;
            font-weight: 300;
            padding: 10px 15px;
            background: #000;           
                    
            @media (max-width: $mobile-break and 1000px) {
                padding: 5px 8px;
                font-size: 8px;
            }               
        }

        #page-developers #block-result {
            margin-top: 40px;
        }

        #page-developers #block-result .title-result {
            font-size: 12px;        
        }    


    </style>

    <link rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.12.0/styles/default.min.css">    

</head>

    <div id="page-developers" class="single-page">
        <div id="block-buttons" class="block-content text-center bg-green block-content">
            <div class="container">
                <div id="form-content-button" class="form-traycheckout text-left clearfix center col-sm-6">
                    <div class="col-sm-12 row">
                        <form id="form-generate-button" class="form-tc " action="" method="post">
                            <fieldset class="block-person form-block-content col-sm-12 row">
                                <div class="form-group col-sm-12 ">
                                    <label class="form-label" for="generator_token_account"> Token de Conta* :</label>

                                    <input id="generator_token_account" class="form-control input-wide" name="generator_token_account" size="40" type="text" value="" placeholder="">

                                </div>
                                <div class="form-group col-sm-12 ">
                                    <label class="form-label" for="generator_product_description"> Nome Produto:</label>

                                    <input id="generator_product_description" class="form-control input-wide" name="generator_product_description" size="80" type="text" value="">
                                </div>
                                <div class="form-group col-sm-12 ">
                                    <label class="form-label" for="generator-product-price"> Valor Produto: </label>

                                    <input id="generator-product-price" class="form-control input-wide" name="generator-product-price" size="10" type="text" value="" data-thousands="." data-decimal="," data-prefix="R$ ">
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
                            <pre><code class="xml hljs" id="result-button">
                            </code></pre>
                        </div>


                    </div>
                </div>         

            </div>
            <div class="divider-bottom-line-green"></div>
        </div>

    </div>
</body>
<script type="text/javascript">
    alert('oi');    

</script>
<script src="/js/highlight.pack.js"></script>         

<script src="https://code.jquery.com/jquery-3.3.1.slim.min.js" integrity="sha384-q8i/X+965DzO0rT7abK41JStQIAqVgRVzpbzo5smXKp4YfRvH+8abtTE1Pi6jizo" crossorigin="anonymous"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.3/umd/popper.min.js" integrity="sha384-ZMP7rVo3mIykV+2+9J3UJ46jBk0WLaUAdn689aCwoqbBJiSnjAK/l8WvCWPIPm49" crossorigin="anonymous"></script>
<script src="https://stackpath.bootstrapcdn.com/bootstrap/4.1.1/js/bootstrap.min.js" integrity="sha384-smHYKdLADwkXOn1EmN1qk/HfnUcbVRZyYmZ4qpPea6sjB/pTJ0euyQp0Mk8ck+5T" crossorigin="anonymous"></script>

<script>
(function( $ ){
  if (!String.prototype.trim) {
    String.prototype.trim = function () {
      return this.replace(/^[suFEFFxA0]+|[suFEFFxA0]+$/g, '');
    };
  }
  function empty(mixed_var) {
    var undef, key, i, len;
    var emptyValues = [undef, null, false, 0, '', '0'];
    for (i = 0, len = emptyValues.length; i < len; i++) {
      if (mixed_var === emptyValues[i]) {
        return true;
      }
    }
    if (typeof mixed_var === 'object') {
      for (key in mixed_var) {
        return false;
      }
      return true;
    }
    return false;
  }

  

  document.addEventListener("DOMContentLoaded", function(event) {
    console.log(hljs)
      hljs.configure({tabReplace: '    '});
      hljs.initHighlightingOnLoad();

      jQuery('#generator-product-price').maskMoney();

      jQuery( "#form-content-button" ).submit(function( event ) {
        event.preventDefault();

        var content = '<form id="form_pagamento" name="form_pagamento" method="post" target="blank" action="https://tc.intermediador.yapay.com.br/payment/transaction"> <input type="hidden" name="token_account" id="token_account" value="{TOKEN_ACCOUNT}"> <input type="hidden" name="transaction_product[][description]" id="product_description" value="{PRODUCT_DESCRIPTION}"> <input type="hidden" name="transaction_product[][quantity]" id="product_quantity" value="1"> <input type="hidden" name="transaction_product[][price_unit]" id="product_price" value="{PRODUCT_PRICE}"> <input type="hidden" name="transaction_product[][extra]" id="product_extra" value=""> <input type="image" src="http://integracao.traycheckout.com.br/btncomprar.png" value="Comprar" alt="Comprar" border="0"> </form>';
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
  });
})(jQuery);  
</script>


