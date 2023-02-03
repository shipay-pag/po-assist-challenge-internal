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

**2) Durante a homologação de um sistema de PDV, você notou o seguinte comportamento durante o PROCESSO DE POOLING¹ do sistema do parceiro:**
¹ Processo de Pooling é o processo em que o PDV fica consultando o status do pedido de 2 em 2 segundos para saber se a cobrança foi paga ou não

```
[03/Feb/2023:00:15:04 +0000] "POST /pdvauth                                   HTTP/1.0" 200 1182 "-" "python-requests/2.24.0" "107.178.207.1
[03/Feb/2023:00:15:04 +0000] "POST /order                                     HTTP/1.0" 200 1182 "-" "python-requests/2.24.0" "107.178.207.1
[03/Feb/2023:00:15:05 +0000] "POST /pdvauth                                   HTTP/1.0" 200 1182 "-" "python-requests/2.24.0" "107.178.207.1
[03/Feb/2023:00:15:05 +0000] "GET /v1/wallets                                 HTTP/1.0" 200 2589 "-" "python-requests/2.24.0" "107.178.207.1
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
