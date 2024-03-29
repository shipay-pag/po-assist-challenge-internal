# PROCESSO SELETIVO INTERNO SHIPAY
# P.O. ASSIST/SUPORTE À INTEGRAÇÃO - 03/02/2023

- Sintam-se a vontade para formular as respostas. Podem responder por extenso, utilizar bullet points, prints, prints comentadas, etc.

---

## 1) O caso abaixo foi reportado pelo DESENVOLVEDOR de um sistema de PDV em um grupo de suporte à integração:

```
pessoal, dúvida:
um cliente fez uma compra de R$ 450,00
ele autoriza a substituir um produto por outro onde faz o pedido ter um total de R$ 500,00

Ou seja, a compra inicial foi de R$ 450, mas a substituição no momento da separação dos produtos, fez a compra subir para R$ 500
é possível ou neste caso o cliente é obrigado a fazer um novo pedido?
```

### Como você responderia?



----
----




## 2) As seguintes descrições das APIs da Shipay constam na nossa documentação oficial. Leia-as atentamente:



**i. API POST /pdvauth**

*Autenticação de PDVs ('Pontos de Venda' ou 'Caixas')*

Serviço de autenticação JWT gerado através das três chaves de autenticação de PDVs (access key, secret key e client id) criadas com o cadastro do cliente (lojista) e suas respectivas lojas e caixas na Shipay.

O access_token retornado por este serviço tem validade de 3 dias e deve ser utilizado para que o PDV autenticado possa realizar as demais chamadas nas APIs da Shipay.

Este serviço de autenticação deve ser chamado em toda abertura do caixa no estabelecimento comercial.

---

**ii. API GET /v1/wallets**

*Lista de carteiras digitais e PSP's associadas à loja*

Este endpoint retorna todas as carteiras digitais que estejam associadas à loja vinculada ao PDV (caixa) autenticado na Shipay.

Este serviço deve ser chamado pelo PDV sempre antes de enviar um pedido (POST /order) para a Shipay. A ideia é que o PDV exiba na tela a lista de carteiras disponíveis e o operador de caixa selecione a carteira informada pelo comprador.

---

**iii. API POST /order**

*Criar um pedido para pagamentos instantâneos.*

Esse serviço cria um pedido no PSP (Pix) ou Carteira Digital informado.

Tem como principais características: aprovação instantânea após o pagamento ser realizado e expiração em 60 minutos. Após a expiração, não será possível pagar os pedidos.

Recomendamos a utilização desse serviço para sistemas de PDV e e-commerce que exijam aprovação instantânea do pagamento quando ele é realizado pelo pagador e confirmado pela Carteira Digital ou PSP (Pix).

---

**iv. API GET /order/<order_id>**

*Retornar o status do pedido para pagamentos instantâneos.*

Este serviço retorna informações de um pedido específico. Deve ser utilizado para consultar o status do pedido após a sua criação e confirmar se o comprador efetuou o pagamento, ou seja, se o status mudou de "pending" para "approved".

IMPORTANTE: As consultas devem ser feitas com intervalos de, no mínimo, 2 segundos entre uma e outra.

----

### Os logs abaixo representam as chamadas que um sistema de PDV está realizando nas APIs da Shipay para realizar uma transação na frente do caixa:

```
[ (dd/mmm/aaaa):(hh:mm:ss) ] "-----------------------API ACIONADA---------------------" DEMAIS INFORMAÇÕES (STATUS CODE, TAMANHO, IP, ETC)

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
**Dicas:**
- Cada linha de log registra uma chamada que o parceiro fez em alguma API
- A ordem cronológica dos eventos é de cima para baixo

----

### Considerando o exposto, você sugeriria alguma melhoria para o sistema de PDV que desenvolveu esta integração? Explique.



----
----




## 3) Durante um dia normal de trabalho, você se depara com as seguintes demandas no mesmo instante:

**i. Dúvida no grupo de Suporte à integração do PDV MaxSystem**
```
pessoal, tentei gerar um pedido no POST /order e recebi a seguinte mensagem de erro:

"message":"The total of the purchase does not match with the sum of the items price"

depodem me ajudar?
```

---

**ii. Dúvida no grupo de Suporte à integração do PDV SmartPDV**
```
bom dia, estou com algumas dúvidas

organizei as dúvidas por tópicos... quando puderem, favor responder

1) É obrigatório a abertura de conta no Banco Original?

2) Essa conta criada no Banco Original, precisará ser apresentada na contabilidade?

3) E se o cliente não quiser de forma alguma abrir uma conta no Banco Original, como atendê-lo?  

4) É obrigatório por lei a instituição financeira informar ao SEFAZ quais transações eletrônicas (cartão de crédito, pix, etc) foram creditadas na conta do contribuinte, baseado nisso, o Banco Original vai informar a SEFAZ sobre os créditos na conta do contribuinte ? Caso positivo, como ficará essa duplicidade de créditos perante os órgãos fiscalizadores, já que o Banco do Brasil fará isso também? 

5) Em nosso exemplo real, foi cadastrada a conta do Banco do Brasil, poderiam nos explicar o porquê da informação dos tokens Client_ID e Client_Secret ? Qual a segurança e garantia nossos clientes terão, com a plataforma obtendo essa informação tão sensível. E se o cliente não tiver esses tokens, o que fazer?

6) Cadastrei duas vezes a mesma conta do Banco do Brasil, como fazer para exclui-la? já que tentei modificar o status nos dois logins e não deu certo;

7) Como fazer para cadastrar a nosso logo? tentei enviar o jpg, mas não está aceitando, conforme imagem acima;

8) Por está apresentando a mensagem  {"code":400,"message":"The total is lower than the minimum payment accepted."} ao tentar criar uma transação, já que o PIX pela legislação pode R$ 0,01 centavos, e tem clientes que vendem chiclete, etc.
```

---

**iii. O PO do Squad Transacional pediu para você fazer um teste da funcionalidade que vai subir no próximo dia**

```
opa <seu nome aqui>, blz?

precisamos testar o card 3358 para fazer o deploy até amanhã para cumprir os prazos combinados com o parceiro, blz? 
```

---

**iv. Um desenvolvedor da squad de cadastro fez uma pergunta sobre um BUG que você reportou no Painel Shipay**
```
Bom dia <seu nome aqui>, td bem?

Vi seu report no grupo, vc consegue mandar o curl da requisição para eu conseguir simular por aqui? Vlw

```

---

**v. O DEV do Sistema de PDV RetailSystem reportou indisponibilidade no ambiente de staging (ambiente de homologação/integração)**
```
pessoal, deste ontem a noite estamos recebendo erro 503 para criar pedidos com expiração variável (POST /orderv)

isso está atrasando nossa integração, podem verificar, por favor?
```

---

### Considerando a situação, qual a ordem de prioridade? 
