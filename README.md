# hub_liveness_samtemplate_lambda (versão 0.0.2)
![](/images/animated.gif)  

### Contato para negociação
milton33b@hotmail.com

### Introdução
O produto HUBIA Liveness é um sofrware que tem como objetivo capturar vários frames de um rosto, dentro de um APLICATIVO Mobile, mandar para o servidor e validar se realmente aquela pessoa está viva (anti-spoofing) e determinar se é a mesma pessoa a partir de uma foto de origem (comparação biometrica, etapa opcional).

Esse é um mecanismo antifraude primordial para automatizar e manter um padrão minímo de segurança ao autorizar transações,logins ou novas aquisições de clientes.

###### Caso de Uso 1
> Você possui um aplicativo financeiro em que o cliente já possui um cadastro.
Quando o cliente fizer o login a partir de um novo dispositivo você deseja adicionar uma camada 
extra de segurança. Então você obriga o cliente a passar pela validação LIVENESS + Comparação biométrica 
baseado na foto que o cliente disponibilizou na hora de fazer o cadastro.

###### Caso de Uso 2
> Você deseja diminuir trabalho humano ao revisar selfies enviadas pelos clientes no momento da aquisição (novo cadastro).
Então você roda somente o sistema de LIVENESS para determinar se aquele cliente está "vivo" ou é uma "foto da foto".

###### Demo Android
https://play.google.com/store/apps/details?id=com.br.hub.liveness.demonstration

### Arquitetura
Todo processamento server-side fica dentro dua sua PROPRIA infraestrutura, ou seja, a HUBIA não possui acesso a nenhum dado ou foto dos seus clientes, garantindo conformidade sobre a LGPD.
Atualmente suportamos apenas stacks dentro da Amazon Web Services:

![Desenho Arquitetura](/images/hubia_liveness_lambda.png)

### Preço
Você paga somente o que consumir dentro da sua propria AWS, mais uma taxa fixa para HUBIA, conforme abaixo:

1. Operações de DynamoDB
2. Operações de Lambda
3. Operações de Rekognition
4. Operações de ApiGateway

###### AWS
1k   validações: USD 6,00    /mensal  
10k  validações: USD 60,00   /mensal  
100k validações: USD 600,00  /mensal  
1kk  validações: USD 6000,00 /mensal  

###### Licenciamento HUBIA
Pay as you go: R$0,05/mensal a cada validação.  
Bloco: R$10000/mensal (dez mil reais) a cada quinhetas mil validações (R$0,02 cada validação).  

###### Similares no mercado
Você teria um custo entre R$0,30 até R$0,80 para para realizar uma validação de liveness + comparação biometrica com ferramentas similares no mercado, exemplificação:

> Hubia: 100k validações  = USD600,00 (AWS) + R$0,05 * 100k =  R$5000,00 (Hubia) + R$3600,00 (AWS) = R$8600,00/Mensal  
> Outros: 100k validações = R$0,30 * 100k = R$30000,00/Mensal  

###### TESTE DE GRAÇA!
Implante e tenha 3 meses de gratuidade sobre o licenciamento HUBIA para qualquer quantidade de requests.
Ou seja, só pague pelo consumo de recursos dentro da sua conta AWS.

### Instalando SAM Template AWS
Para começar, primeiro você deve instalar o software HUBIA dentro da sua conta AWS. Vamos fazer isso através de uma stack cloudformation, com um arquivo SAM template.

1. Faça o download do template.yml: https://hublia-liveness-deploys.s3.amazonaws.com/0.0.2/template.yml  
2. Abra o seu console AWS (tenha permissão de administrador) -> Cloudformation -> https://console.aws.amazon.com/cloudformation/home  
3. Escolha um nome para sua STACK. Todos os recursos criados, serão tageados com esse nome  
![](/images/tuto-cf-create4.png)  
4. Clique no botão "create stack" -> With new Resources   
![](/images/tuto-cf-create1.png)  
5. Upload a template file -> Upload file (faça o upload do arquivo que você baixou no passo 1)  
![](/images/tuto-cf-create2.png)  
6. Preencha os parametros:  
![](/images/tuto-cf-create3.png)  

AuthPassword: Isso será fornecido pela HUBIA.  
AuthUsername: Isso será fornecido pela HUBIA.  
Environment: Coloque PRD  
S3BucketName: Nome do bucket que será criado na sua conta  
PrivateIpMask: Coloque o IP que estará autorizado a fazer chamadas privadas (para startar a transação do cliente, normalmente o IP do seu servidor de produção)   

--- Importante:
Caso queira deixar aberto para internet toda, coloque: 0.0.0.0/0
Mas só faça isso em cenários controlados de testes...

7. Passe por todas as telas sem mexer em nada e clique em "Create Stack":
![](/images/tuto-cf-create5.png)

8. Aguarda a stack ser executada por completo e clique na aba "outputs" para pegar os endpoints das APIs:
![](/images/tuto-cf-create6.png)

Pronto! Você completou a instalação da HUBIA do lado servidor.

### Integraçõs HTTP privadas
https://documenter.getpostman.com/view/18132126/UVC5FTSH

### Integração Android
-- Em construção

### Integração IOS
-- Em construção