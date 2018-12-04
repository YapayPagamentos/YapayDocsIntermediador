# Notificação Automática de Status

Para realizar a atualização automática do pedido, a Yapay pode realizar a comunicação a cada alteração de status de uma transação, 
fazendo com que seu sistema acompanhe todo o fluxo de status e esteja sempre atualizado quanto a situação da transação.

Dessa forma você precisa configurar uma URL que receberá a chamada, processará os dados recebidos, 
e em seguida irá obter mais detalhes da transação através da [**API de Consulta de Transação**](api-consultar-transacao.md). 
Esse parâmetro está disponível em ambas as integrações (POST ou API) e chama-se `transaction[url_notification]`.
