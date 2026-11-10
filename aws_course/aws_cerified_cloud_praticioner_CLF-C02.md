## O que é Cloud Computing?
é augar recursos de T.I(servidor, armazenamento, banco de dados) pela internet e pagar apenas pelo que usar, ao invés de comprar e manter servidor próprio.

**Pontos chaves:**
- sob demanda (cria em minutos);
- paga pelo uso;
- escala para cima ou para baixo fácil;
- sem datacenter próprio para manter.

**3 modelos:**
- **IaaS:** aluga a infra (ex: EC2);
- **PaaS:** só sobe o código (ex: Elastic Beanstalk);
- **SaaS:** software pronto (ex: gmail).

**Segurança**: a aws cuida *da* núvem (hardware), você cuida *na* núvem (seus dados e acessos).

## Como surgiu a AWS?
a AWS foi lançada oficialmente em 2006, o motivo é que a Amazon (loja online) precisou construir uma infraestrutura gigante e eficiente para aguentar o prório e-commerce. Depois disso, eles perceberam que toda a emrpesa perdia muito tempo e dinheiro montando infraestrutura antes de criar o produto em si. Foi aí que decidiram vender essa infraestrutura como serviço, pagando só pelo uso. Ou seja, a Amazon aprendeu a rodar infraestrutura em larga escala para o seu e-commerce e transformou isso em produto, foi aí que nasceu a AWS.

## Tipos de cloud:
- **pública:** essa é onde entra a AWS, GCP, Azure. Ser pública não significa que os dados serão expostos na internet para qualquer um acessar. Ser pública significa que a Amazon AWS por exemplo vai dividir todo o servidor dela em partes para várias pessoas, e você ficará com uma dessas partes. Resumindo, nesse tipo você não compra hardware, nesse tipo você só paga pelo uso.
- **privada:** nesse modelo a empresa mantem o seu data center próprio (ex: bancos, alguns hospitais). Isso significa que a empresa monta todo o seu hardware.
- **hibrida:** nesse modelo a empresa mistura os outros dois, ou seja, ela tem parte na cloud e parte no ambiente próprio.

## Vantagens de se utilizar cloud:
- **on demand:** você cria o serviço e paga apenas pela utilização dele (minutos ou segundos) ou seja, se você usar um serviço apenas por 12h, você paga apenas por essas 12h.
- **elasticidade:** você pode aumentar ou reduzir o recurso de acordo com a sua necessidade.
- **acesso global:** disponível de qualquer lugar. Ou seja, você pode criar uma aplicação no Brasil e replicar a conexão para outro pais.

## Completando algumas tarefas:
quando criamos a conta da AWS no *Free Tier**, nós temos 100 dolares de crédito para estudar na plataforma, porém, se a gente completar algumas tarefas, ganhamos 20 dolares por cada uma, no total são 5, 100 dolares a mais.

- **Configurar um orçamento de custos utilizando o _AWS Budgets_**: primeiro nós vamos em *gerenciamento de faturamento e custos*. Depois damos um nome, tipo *"alerta"*. Depois colocamos o e-mail que vamos receber o alerta. Depois clicamos em *criar orçamento*.
- **Iniciar uma instância _EC2_**: importante, criar uma instancia vai descontar dos créditos, mas vamos ganhar os 20 dolares por concluir essa tarefa. Primeiro damos um nome para a instancia, ex: *"instancia de teste"*. Depois orecisamos escolher a imagem do sistema operacional. Depois escolhemos uma *"AMI"*. Aí escolhemos o hardware, o recomendável para esse exemplo é escolher o hardware mais leve, assim o gasto é menor. Depois criamos um novo par de chaves para usar na instância, baixamos e guardamos a chave, pois usaremos ela para se conectar na instância, logo após selecionamos as chaves. Depois configuramos a rede, a própria AWS alerta que para esse tutorial é tudo bem usar as configurações padrões de rede pública, mas para um projeto em produção deve-se atribuir um IP público, usar uma sub-rede e usar acesso a internet somente quando for absolutamente necessário. Depois configuramos o Firewall, a AWS também alerta que para essa instância de teste, não tem problema permitir a conexão de qualquer IP, mas para um projeto em produção, temos que usar um IP confiável. Logo após isso escolhemos a configuração de armazenamento, para produção é recomendável um armazenamento criptografado, mas para esse teste não precisa. Após isso revisamos as configurações e criamos a instância. A AWS recomenda criar um alerta de faturamento, então clicamos em *"alerta de faturamento"* e em *"preferências de alerta"* nós marcamos *"alerta do nível gratuito da AWS"* e colocamos o e-mail,após isso marcamos *"alerta de faturamento do cloud watch"*. Depois conectamos a instância clicando em *"conectar-se a instância"*. Após fazer o teste podemos deletar a instância. Clicamos no id dela e vamos para a página, lá clicamos em *"estado da instância"*, clicamos para encerrar e confirmamos em encerrar novamente.
- **Criar uma base de dados no _Aurora_ ou _RDS_**: primeiramente precisamos escolher qual banco iremos utilizar, a própria AWS alerta que essa atividade pode ter cobrança. Depois escolhemos o metodo de criação do banco. Após isso, devemos reisar a configuração. Por fim, clicamos no botão de criar banco de dados.
- **Criar uma aplicação web utilizando o _AWS Lambda_**: primeiro damos um nome, no exemplo eu coloquei apenas *"teste"*. Depois eu mantive o padrão da origem do código como *"modelo hello world"*. Depois coloquei o nome do endpoint como *"teste"*. Selecionei o tipo da autenticação. Por fim criei a função.
- **Utilizando um modelo de base no playground _Amazon Bedrock_**: primeiro eu seleciono o modelo, escolhi *Claude Haiku*, preenchi algumas informações, criei e testei com um prompt.

## Tarefas concluídas.