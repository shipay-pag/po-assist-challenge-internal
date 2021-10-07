#### Teste PO Assist - Processo Seletivo Interno:

- Sintam-se a vontade para formular as respostas. Podem responder por extenso, utilizar bullet points, prints, prints comentadas, etc.



#### 1) Ao navegar pelo Painel Shipay, você, integrante do time de produtos da Shipay, se depara com o famoso erro "OK". Como você reportaria esse caso para o time de desenvolvimento?



#### 2) Precisamos atualizar nossa documentação, pois o serviço Pix Cobrança com Vencimento no Padrão Bacen já está disponível! Leia um trecho de uma reportagem da InfoMoney sobre esse serviço:


>O Pix Cobrança com Vencimento vai permitir fazer um pagamento usando Pix em uma data futura. O Pix Cobrança com Vencimento pode ser usado por lojistas, >fornecedores, prestadores de serviços e usuários pessoas físicas.

>Empresas ou microempreendedores, por exemplo, poderão emitir um código QR para transações que serão cobradas dos clientes em data futura, como se fosse uma >versão mais moderna de um boleto. Do ponto de vista das pessoas físicas, será mais uma alternativa de pagamento de compras e contas a prazo.

>Igor Senra, CEO da fintech Cora, explica que o QR Code poderá aparecer em pontos de venda, em e-commerces e na hora de cobrar serviços, já com a data de >vencimento da conta. Esse QR Code estará disponível tanto na posição horizontal quanto na vertical. Ao comprar um sapato em um e-commerce, por exemplo, a pessoa >poderá escolher o Pix Cobrança entre os meios de pagamentos no lugar de um boleto.

>Desde o lançamento do Pix, só era possível gerar um código QR para pagamentos imediatos. Além da possibilidade de pagar em uma data futura, a diferença para esse >nova modalidade é a inclusão de mais informações fora o valor, como juros, multa e descontos. Assim, o Pix Cobrança se torna de fato uma alternativa ao boleto.

Uma documentação de uma API, geralmente conta com uma descrição geral que contemple as principais características do serviço, além do detalhamento técnico de cada componente do contrato da API. Dê uma olhada na forma como escrevemos a descrição do serviço de Cobranças Para Pagamento Instantâneo:

- Com essas informações em mãos, como você documentaria somente a descrição do serviço Pix Cobrança com Vencimento (Padrão Bacen)?




#### 3) Você está tentando criar um pedido de teste via Postman, em um cliente que acabou de ser cadastrado na Shipay. Ao enviar a requisição, recebe o seguinte retorno do POST /order: 

HTTP status code: 400 

{
    "message": "Order not created"
}

Sabemos que o erro 400 com essa mensagem é pouco conclusivo e que vai ser necessário uma investigação um pouco mais aprofundada para entender o motivo do erro. 

O que você faria para investigar o motivo do erro? Por quê seguiria essa estratégia?
