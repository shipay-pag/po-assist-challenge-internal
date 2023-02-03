**PROCESSO SELETIVO INTERNO SHIPAY - P.O. ASSIST/SUPORTE À INTEGRAÇÃO - 03/02/2023**

- Sintam-se a vontade para formular as respostas. Podem responder por extenso, utilizar bullet points, prints, prints comentadas, etc.


**1) O caso abaixo foi reportado pelo DESENVOLVEDOR de um sistema de PDV em um grupo de suporte à integração:**

```
pessoal, dúvida:
um cliente fez uma compra de R$ 450,00
ele autoriza a substituir um produto por outro onde faz o pedido ter um total de R$ 500,00

Ou seja, a compra inicial foi de R$ 450, mas a substituição no momento da separação dos produtos, fez a compra subir para R$ 500
é possível ou neste caso o cliente é obrigado a fazer um novo pedido?
```

**Como você responderia?**



----
----



**2) As seguintes descrições das APIs da Shipay constam na nossa documentação oficial. Leia-as atentamente:**
.
.
.
**i. Serviço POST /pdvauth**

*Autenticação de PDVs ('Pontos de Venda' ou 'Caixas')*

Serviço de autenticação JWT gerado através das três chaves de autenticação de PDVs (access key, secret key e client id) criadas com o cadastro do cliente (lojista) e suas respectivas lojas e caixas na Shipay.

O access_token retornado por este serviço tem validade de 3 dias e deve ser utilizado para que o PDV autenticado possa realizar as demais chamadas nas APIs da Shipay.

Este serviço de autenticação deve ser chamado em toda abertura do caixa no estabelecimento comercial.
.
.
.
**ii. Serviço POST /order**

*Criar um pedido para pagamentos instantâneos.*

Esse serviço cria um pedido no PSP (Pix) ou Carteira Digital informado.

Tem como principais características: aprovação instantânea após o pagamento ser realizado e expiração em 60 minutos. Após a expiração, não será possível pagar os pedidos.

Recomendamos a utilização desse serviço para sistemas de PDV e e-commerce que exijam aprovação instantânea do pagamento quando ele é realizado pelo pagador e confirmado pela Carteira Digital ou PSP (Pix).
.
.
.
**iii. Serviço GET /order/<order_id>**

*Retornar o status do pedido para pagamentos instantâneos.*

Este serviço retorna informações de um pedido específico. Deve ser utilizado para consultar o status do pedido após a sua criação e confirmar se o comprador efetuou o pagamento, ou seja, se o status mudou de "pending" para "approved".

IMPORTANTE: As consultas devem ser feitas com intervalos de, no mínimo, 2 segundos entre uma e outra.
.
.
.
----

Os logs abaixo representam as chamadas que um sistema de PDV está realizando nas APIs da Shipay para realizar uma transação na frente do caixa:



```
[03/Feb/2023:00:15:04 +0000] "POST /pdvauth                                   HTTP/1.0" 200 1182 "-" "python-requests/2.24.0" "107.178.207.1
[03/Feb/2023:00:15:04 +0000] "GET /v1/wallets                                 HTTP/1.0" 200 2589 "-" "python-requests/2.24.0" "107.178.207.1
[03/Feb/2023:00:15:05 +0000] "POST /pdvauth                                   HTTP/1.0" 200 1182 "-" "python-requests/2.24.0" "107.178.207.1
[03/Feb/2023:00:15:05 +0000] "POST /order                                     HTTP/1.0" 200 1182 "-" "python-requests/2.24.0" "107.178.207.1
[03/Feb/2023:00:15:06 +0000] "POST /pdvauth                                   HTTP/1.0" 200 1182 "-" "python-requests/2.24.0" "107.178.207.1
[03/Feb/2023:00:15:06 +0000] "GET /order/f04e1945-3088-4dd3-8818-817ab98a8357 HTTP/1.0" 200 579 "-" "python-requests/2.24.0" "107.178.207.1
[03/Feb/2023:00:15:07 +0000] "POST /pdvauth                                   HTTP/1.0" 200 1182 "-" "python-requests/2.24.0" "107.178.207.1
[03/Feb/2023:00:15:07 +0000] "GET /order/f04e1945-3088-4dd3-8818-817ab98a8357 HTTP/1.0" 200 579 "-" "python-requests/2.24.0" "107.178.207.1
[03/Feb/2023:00:15:08 +0000] "POST /pdvauth                                   HTTP/1.0" 200 1182 "-" "python-requests/2.24.0" "107.178.207.1
[03/Feb/2023:00:15:08 +0000] "GET /order/f04e1945-3088-4dd3-8818-817ab98a8357 HTTP/1.0" 200 579 "-" "python-requests/2.24.0" "107.178.207.1
[03/Feb/2023:00:15:09 +0000] "POST /pdvauth                                   HTTP/1.0" 200 1182 "-" "python-requests/2.24.0" "107.178.207.1
[03/Feb/2023:00:15:09 +0000] "GET /order/f04e1945-3088-4dd3-8818-817ab98a8357 HTTP/1.0" 200 579 "-" "python-requests/2.24.0" "107.178.207.1
[03/Feb/2023:00:15:10 +0000] "POST /pdvauth                                   HTTP/1.0" 200 1182 "-" "python-requests/2.24.0" "107.178.207.1
[03/Feb/2023:00:15:10 +0000] "GET /order/f04e1945-3088-4dd3-8818-817ab98a8357 HTTP/1.0" 200 579 "-" "python-requests/2.24.0" "107.178.207.1
[03/Feb/2023:00:15:11 +0000] "POST /pdvauth                                   HTTP/1.0" 200 1182 "-" "python-requests/2.24.0" "107.178.207.1
[03/Feb/2023:00:15:11 +0000] "GET /order/f04e1945-3088-4dd3-8818-817ab98a8357 HTTP/1.0" 200 579 "-" "python-requests/2.24.0" "107.178.207.1
```
