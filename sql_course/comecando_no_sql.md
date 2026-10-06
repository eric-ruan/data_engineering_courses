# O que são banco de dados:
- Qualquer formato onde se possa armazenar um dados, seja esse formato um caderno, uma lista de compras ou até mesmo um sistema em um computador ou servidor.

# Diferença entre *SQL* e *NoSQL*:
- **SQL**: é uma linguagem de banco de dados relacional, que funciona para fazer consultas estruturadas. Qualquer projeto onde precisa ter uma relação, pode-se usar bancos de dados relacionais, ou seja, SQL.
- **NoSQL**: ele armazena informações em formato de documento. Pode-se armazenar muitas informações e elas não precisam ser estruturadas.

# O que é uma *DBMS*:
- **Database management system** é um gerenciador de banco de dados, como: *MySQL, Postgre, etc*...

# Informações dentro de uma tabela:
Uma tabela é constituída por coluna **(atributo)** e linhas **(tuplas)**. Geralmente a primeira coluna está identificada como **"id"**, ela é a **primary key**. Os dados dentro de uma coluna são chamados de **"data value"**.

# Tabelas relacionais e Keys:
Em banco de dados relacional, pode parecer obvio, mas as tabelas tem uma relação entre elas.
- A **primary key** é usada para se relacionar com outra tabela.
- A **foreing key** são chaves importantes de outra tabela.

Basicamente a função de se ter **chave primária** e **chave estrangeira** em um banco, é para deduzir o tamanho total desse banco evitando duplicidades de dados.

# Utilizando o *USE* e o *SELECT*:
- **USE**: esse comando serve para dizer qual banco queremos usar. No exemplo do curso:
```sql
USE sakila;
```
- **SELECT**: esse comando serve para fazer consultas no banco, visualizar alguma informação. No exemplo do curso:
```sql
SELECT actor_id FROM actor;
```

# Utilizando o *ORDER BY*
- **ORDER BY**: esse comando serve para ordenar a consulta, exemplo:
se eu quero fazer uma consulta com o *SELECT* e ordenar o campo de nome em ordem alfabética eu uso:
```sql
SELECT actor_id, first_name, last_name
FROM actor
ORDER BY first_name
```
dessa forma, toda a consulta estará em ordem alfabética pelo first_name.

# Adicionando *WHERE* e *comentando uma linha*:
- **WHERE**: esse comando é uma condição, ou em outras palavras, um filtro para a consulta. Com ele podemos filtrar um determinado valor, ou seja, só será retornado os valores que atendam aquela condição.
- **Para comentar** uma linha, usa-se **--**

exemplo dos dois casos:
```sql
SELECT actor_id, first_name, last_name
FROM actor
WHERE actor_id <= 10
```
**O que acontece nessa consulta:** o banco retorna apenas os 10 primeiros reistros da tabela *actor*. Isso em ordem de *actor_id*, porque foi usado **"--"** para comentar a linha do ```ORDER BY```.
**Importante: se você quer os 10 primeiros registros usado o ```ORDER BY```, é preciso declarar ```<=```, se não o banco me retorna apenas os 9 primeiros.**

# Modificando uma colunas "apenas para visualização":
Nas consultas, nós podemos criar novas colunas com cálculos ou com qualquer outra coisa que desejarmos. No exemplo abaixo, eu criei uma nova coluna de visualização, onde eu vou dar 10% de desconto no valor pago pelo cliente.
**Importante**: essa nova coluna é apenas para consulta. Ela não modifica o banco.
```sql
SELECT
    customer_id,
    amount,
    amount - (amount * 0.10) AS '10% discount'
FROM payment
WHERE customer_id = 1
```
Basicamente, o que eu fiz é criar uma coluna com 10% de desconto nas compras do cliente cujo id = 1. Também estou renomeando essa coluna com o ```AS``` colocando nela o nome de *'10% discount'*.

# Mais variações do *WHERE*:
Por ser uma condição nas consultas, o ```WHERE``` pode ser usado de diversas formas. Por exemplo, se eu quiser consultar os maiores valores da tabela, eu posso primeiro fazer uma consulta usando o ```ORDER BY```.
```sql
SELECT customer_id, amount
FROM payment
ORDER BY amount DESC
```
Dessa forma eu consigo ver que o maior valor é *11.99*. Assim eu consigo usar o ```WHERE``` e buscar todos os clientes que pagaram *11.99*.
```sql
SELECT customer_id, amount
FROM payment
-- ORDER BY amount DESC
WHERE amount = 11.99
```

# Operadores *AND*, *OR* e *NOT*
- **AND**: significa quando você quer uma condição **E** outra, por exemplo, se eu quiser saber os registros do funcionário número 1 que fez vendas de 0.99, eu faço:
```sql
SELECT *
FROM payment
WHERE staff_id = 1 AND amount = 0.99
```
- **OR**: significa quando você quer a opção **A** ou a opção **B**, exemplo:
```sql
SELECT *
FROM payment
WHERE staff_id = 1 OR amount = 0.99
```
**O que acontece nessa condição é:** por mais que tenha casos onde o *id* é 2, se o *amount* for 0.99 a consulta mostra. Ou seja, **ou um ou outro**.
- **NOT**: serve para negar uma condição, ele pode ser usado de duas formas, assim: *NOT* ou assim: *!=*. Dessa forma quando fizer uma consulta o banco vai me retornar todos os valores que **NÃO** sejam aquele que está sendo negado, exemplo:
```sql
SELECT *
FROM payment
WHERE NOT staff_id = 1
```
O resultado é todos os *ids* que não sejam 1, pois eu estou negando que seja 1.

# Operador *IN*:
Esse operador é bem parecido com o *OR*, a diferença é que com o *IN*, nós conseguimos colocar vários valores na mesma frase, exemplo:
```sql
SELECT *
FROM address
WHERE district IN ('Alberta', 'California')
```
Ou seja, com o *IN* nós conseguimos passar como valor uma tupla, coisa que com o *OR* teríamos que passar vários valores assim:
```sql
Cidade = 'Alberta'
Cidade = 'California'
```

# Operador *BETWEEN*:
Como o nome já sugere, esse operador é para quando se quer filtrar dois valores, exemplo: se eu quiser consultar na tabela de pagamentos, valores que estão entre *0.99* e *3.99*. Eu faço:
```sql
SELECT *
FROM payment
WHERE amount BETWEEN 0.99 AND 3.99
```
Dessa forma a consulta vai me retornar valores que são *>=* à 0.99 e *<=* a 3.99 (os dois extremos entram no resultado). Esse operador ajuda a deixar os códigos mais limpos, ao invés de usar o *AND* para tudo.

# Operador *LIKE*:
O operador *LIKE* é diferente de usar o *=*. Enquanto o *=* só aceita caracteres identicos, com o *LIKE* você tem mais flexibilidade, exemplo: se eu quiser descobrir o nome de algum *actor* que comece com a letra *'P'* eu uso o *LIKE 'P%'*, dessa forma ele mostra os atores e atrizes que a primeira letra do nome é *P*:
```sql
SELECT *
FROM actor
WHERE first_name LIKE 'P%'
```
Também podemos usar isso para que tenhamos visualização de nomes que terminam com alguma letra, por exemplo:
```sql
SELECT *
FROM actor
WHERE first_name LIKE '%E'
```

# Operador *IS NULL*:
Esse operador serve para buscar no banco registros que sejam nulos, também podemos usar para registros que sejam *não nulos* negando o operador. Para usa-lo, fazemos:
```sql
SELECT *
FROM address
WHERE address2 IS NULL
```

# Operador *LIMIT*:
Serve para fazer uma consulta limitando o tanto de registros que será mostrado, exemplo: se eu quero fazer uma consulta mostrando 10 registros a partir do registro de número 5, fazemos:
```sql
SELECT *
FROM actor
LIMIT 5, 10
```
Dessa forma eu visualizo os *ids* 6 até o 15.

# Operador *REGEXP*:
Esse operador serve para fazer consultas com *expressão regular*, ou seja, consultas complexas, exemplo:
```sql
WHERE nome REGEXP '^[0-9]{5}-[0-9]{3}$'
```
Traz só ceps no formato *00000-000*
```sql
WHERE nome REGEXP '[aeiou]$'
```
Traz nomes que terminam com vogal.

**Simbolos:**
- **^** começo
- **$** final
- **|** ou
- **[]** um desses caracteres

# Operadores matemáticos:
Nós podemos usar os operadores matemáticos para criar expressões, eles são:
- **+** somar
- **-** subtrair
- **\*** multiplicar
- **/** dividir

Eles só funcionam em colunas do tipo numérico.

# Operadores de comparação:
Eles são usados para comparar um valor com o outro:
- **=** igual A
- **>** maior que
- **>=** maior ou igual a
- **<** menor que
- **<=** menor ou igual a
- **<>** diferente de

# Operadores lógicos:
Eles servem para fazer com que duas condições produzam um resultado único. Os dados só serão retornados se o resultado global da condição for verdadeiro.
- **AND**: retorna *TRUE* se ambas as condições forem verdadeiras.
- **OR**: retorna *TRUE* se uma das condições forem verdadeiras.
- **NOT**: retorna *TRUE* se a condição seguinte for falsa.

# *INNER JOIN*:
Ele serve para juntar dados de duas tabelas, retornando a linhas que tem correspondência entre elas:
```sql
SELECT *
FROM customer
INNER JOIN payment ON customer.customer_id = payment.customer_id
```
Afora se quisermos fazer filtros nessa consulta, para retornar valores que queremos ver, fazemos assim:
```sql
SELECT
    customer.customer_id,
    customer.first_name,
    customer.last_name,
    payment.rental_id,
    payment.amount
FROM customer
INNER JOIN payment ON customer.customer_id = payment.customer_id
```
Podems também dar um  nome para as tabelas, assim não precisamos ficar digitando os nomes delas à todo momento. Isso se chama *Alias*.
```sql
SELECT
    cus.customer_id,
    cus.first_name,
    cus.last_name,
    pay.rental_id,
    pay.amount
FROM customer AS cus
INNER JOIN payment AS pay ON cus.customer_id = pay.customer_id
```
Nós podemos também usar vários *JOINs* em uma consulta, podemos fazer com 3 tabelas ou mais, segue o exemplo com 3 tabelas:
```sql
SELECT
    cus.customer_id,
    cus.first_name,
    cus.last_name,
    pay.rental_id,
    pay.amount
FROM customer AS cus
INNER JOIN payment AS pay
    ON cus.customer_id = pay.customer_id
INNER JOIN address AS adr
    ON cus.address_id = adr.address_id
```
# Adicionando uma linha na tabela:
Para inserir dados em uma tabela nós usamos o ```INSERT INTO```. Primeiro é interessante rodar o comando: ```DESCRIBE banco.tabela``` para ter as informações da tabela. Nós também não precisamos preencher com valor o campo que é *"auto-increment"*, para isso usamos o *"DEFAULT"*:
```sql
INSERT INTO language
VALUES(DEFAULT, 'Portuguese', '2026-10-01 17:10:19');
```

# Inserindo várias linhas à uma tabela:
Para isso, basta copiar o comado *VALUES*. Em outras palavras, basta inserir várias tuplas:
```sql
INSERT INTO language
VALUES
    (DEFAULT, 'Spanish', '2026-10-01 17:20:00'),
    (DEFAULT, 'Polish', '2026-10-01 17:30:00');
```

# Inserindo dados em múltiplas tabelas:
Isso é necessário porque as vezes queremos fazer inserção de dados em uma tabela que tem relacionamento com outra tabela. No exemplo abaixo, eu quero inserir uma nova cidade na tabela *"city"*, mas nessa tabela tem uma coluna *"country_id"*, ou seja, uma tabela está se relacionando com a outra. Para resolver esse problema nós usamos uma função do SQL que se chama *"LAST_INSERT_ID()"*. O script vai ficar assim:
```sql
INSERT INTO country
VALUES
    (DEFAULT, 'Brasil2', '2026-10-01 18:55:20');

INSERT INTO city
VALUES
    (DEFAULT, 'Sao Paulo2', LAST_INSERT_ID(), '2026-10-01 18:55:20');
```

# Copiar uma tabela:
Tem diversos motivos pelos quais fazer a cópia de uma tabela. Um desses é para backup. Para fazer isso, basta usar o comando abaixo:
```sql
CREATE TABLE payment_backup AS
SELECT * FROM payment
```
Basicamente você digita o comando para criar a tabela e passa o *SELECT* para o banco retornar a tabela que você quer copiar.

# Removendo uma tabela:
Existem dois tipos de remoção:
- **TRUNCATE TABLE**: apaga todos os dados da tabela deixando-a vazia, mas com toda a estrutura, ou seja, as colunas.
```sql
TRUNCATE TABLE payment_backup;
```

- **DROP TABLE**: remove todo o esquema da tabela, ou seja, apaga todos os dados e exclui a tabela.
```sql
DROP TABLE payment_backup;
```

# Atualizando um valor:
Se eu quero alterar um determinado valor de uma tabela, eu uso o comando *UPDATE*, no exemplo abaixo, eu estou alterando o *"amount"* para *15.99* no *id 1*.
```sql
UPDATE payment
SET
    amount = 15.99
WHERE
    payment_id = 1;
```
Também podemos alterar várias linhas de uma só vez, apenas colocando os outros valores em baixo e separando por vírgula, assim:
```sql
UPDATE payment
SET
    amount = 15.99,
    payment_date = '2026-01-01 01:01:01',
    last_update = '2026-10-01 20:15:00'
WHERE
    payment_id = 2;
```

# Deletando um valor:
Como o nome já sugere, esse comando serve para deletar um valor na tabela. Para isso, fazemos assim:
```sql
DELETE FROM payment
WHERE payment_id = 16049;
```
Nesse exemplo de cima eu estou deletando a linha do **id 16049**.

# Introdução a funções:
Funções basicamente são códigos que já estão criados e prontos para nós usarmos.

# Aplicando funções básicas:
Nesse exemplo abaixo temos 3 problemas, eu quero saber qual foi a minha **maior venda**, a minha **menor venda** e a **média de vendas**. Funções:
- **MAX()**: serve para consultar o valor máximo de uma coluna, nesse caso o valor da maior venda:
```sql
SELECT MAX(amount) AS Maior
FROM payment;
```

- **MIN()**: serve para consultar o valor mínimo de uma coluna, nesse caso o valor da menor venda:
```sql
SELECT MIN(amount) AS Menor
FROM payment;
```

- **AVG()**: serve para consultar o valor médio de uma coluna, nesse caso a média de vendas:
```sql
SELECT AVG(amount) AS Media
FROM payment;
```

# Utilizando o *COUNT()* e o *SUM()*
Como os próprios nomes sugerem, essas funções são de **contagem** e **soma**.
- **COUNT()**: é usado para contar valor em uma coluna, no exemplo abaixo eu estou querendo saber o total de vendas:
```sql
SELECT COUNT(amount) AS 'Numero de Vendas'
FROM payment;
```

- **SUM()**: é usado para somar valores em uma coluna, no exemplo abaixo eu estou querendo saber a soma total de vendas:
```sql
SELECT SUM(amount) AS 'Total de Vendas'
FROM payment;
```
Nós também podemos usar o *WHERE* para fazer filtros na tabela, por exemplo, saber o valor total de vendas e a quantidade de vendas de uma determinada pessoa, usamos:
```sql
SELECT
    COUNT(amount) AS 'Numero de Vendas',
    SUM(amount) AS 'Total de Vendas'
FROM payment
WHERE staff_id = 1
```

# Agrupando os clientes:
Nessa etapa nós vamos ver quanto cada cliente gastou dentr da locadora. Por exemplo, eu quero saber quanto o cliente *1* gastou, quanto o cliente *2* gastou e assim por diante. Também quero ordenar os valores do mais gasto para o menos gasto. Para isso, vamos usar uma função, a de soma *SUM()*, usar o *GROUP BY* e usar o *ORDER BY*, ficando assim:
```sql
SELECT
    customer_id,
    SUM(amount) AS Total
FROM payment
GROUP BY customer_id
ORDER BY Total DESC;
```

# Ordenando os clientes:
Imaginemos que o time de marketing pede um relatório para entender quem foi os clientes que mais compraram, mas eles não querem saber o *ID* desses clientes, eles querem saber o nome. Então nesse caso fazemos um *INNER JOIN* de duas colunas, a de **customer** e a de **payment** e depois ordenamos:
```sql
SELECT
    cus.customer_id AS ID,
    cus.first_name AS Nome,
    cus.last_name AS Sobrenome,
    SUM(pay.amount) AS Total
FROM payment AS pay
INNER JOIN customer AS cus
ON cus.customer_id = pay.customer_id

GROUP BY ID
ORDER BY Total DESC
```

# Filtrando os valores com *HAVING*:
Nesse problema, nós precisamos mostrar em resultado os clientes que gastaram mais de *$150 dolares*. Nesse caso nós não usaremos o *WHERE* e sim o *HAVING*. Além disso, irei mostrar no relatório também o valor total de compras do cliente, mas dessa vez, vou exibir apenas os clientes que tiveram mais de *35 compras*. Fica assim:
```sql
SELECT
    cus.customer_id AS ID,
    cus.first_name AS Nome,
    cus.last_name AS Sobrenome,
    SUM(pay.amount) AS Total,
    COUNT(pay.amount) AS Compras
FROM payment AS pay
INNER JOIN customer AS cus
ON cus.customer_id = pay.customer_id

GROUP BY ID
HAVING Total >= 150 AND Compras >= 35
ORDER BY Total DESC
```

# Realizando o *DROP* do banco:
Para excluir um banco de dados, usamos o seguinte comando:
```sql
DROP DATABASE banco;
```
**IMPORTANTE**: isso apaga o banco por completo, então só deve ser feito com a certeza total de que realmente é isso que quer.

# Importando um DataBase:
O sistema operacional que eu uso é o Linux, mas no Windows é os mesmos comandos:
- Primeiro nós precisamos logar no MySQL, então basta abrir o Terminal no meu caso ou o CMD no Windows:
```sql
mysql -u usuario -p
```
- Depois nós rodamos o seguinte comando, para acessar o local onde os arquivos do banco foram extraídos. Esse comando já cria o schema do banco Sakila:
```sql
SOURCE caminho/sakila-db/sakila-schema.sql;
```
- Depois nós rodamos o comando para adicionar os dados ao banco:
```
SOURCE caminho/sakila-db/sakila-data.sql;
```

# Criando uma *SubQuery*
Uma **SubQuery** basicamente é o processo de colocar uma query dentro de outra query, o resultado da de dentro é usado pela de fora. No exemplo abaixo eu quero os valores da coluna *amount* que sejam maiores que os valores da média da coluna *amount*, segue o exemplo:
```sql
SELECT *
FROM payment
WHERE amount > (
    SELECT AVG(amount)
    FROM payment
);
```

# Trabalhando com o *MAX* em *SubQuery*:
Esse comando como o próprio nome diz, ele serve para buscar o maior valor de uma coluna, por exemplo, se eu quiser saber a maior venda de um determinado cliente, eu posso fazer assim:
```sql
SELECT MAX(amount)
FROM payment
WHERE customer_id = 1
```
Mas e se eu quiser saber quais são os valores da cluna que são iguais a esse de cima? As vezes esse é um dado impotante para se ter em um relatório, para isso fazemos assim:
```sql
SELECT *
FROM payment
WHERE amount = (
    SELECT MAX(amount)
    FROM payment
    WHERE customer_id = 1
)
```

# Utilizando o *IN*:
Vamos criar um problema para que a explicação fique mais fácil:
- Vamos supor que eu quero a média de compras por *ID*. Mas não quero saber apenas o número, quero saber o *nome* e o *sobrenome*, e quero que me retorne apenas os clientes onde o número de compras seja maior que 35, para isso fazemos assim:
```sql
SELECT customer_id, first_name, last_name, email
FROM customer
WHERE customer_id IN (
    SELECT customer_id
    FROM payment
    GROUP BY customer_id
    HAVING COUNT(*) > 35
)
```
Dessa forma conseguimos ver informaçã de todos os clientes que fizeram mais de 35 compras.

# Utilizando o *ANY*:
Basicamente podemos fazer a mesma coisa que foi feito com o *IN*, o *ANY* significa *"qualquer um"*:
```sql
SELECT customer_id, first_name, last_name, email
FROM customer
WHERE customer_id = ANY(
    SELECT customer_id
    FROM payment
    GROUP BY customer_id
    HAVING COUNT(*) > 35
)
```
O que o código faz é me mostrar qualquer um que esteja dentro do contador de compras acima de 35.

# Criando a primeira *VIEW*:
As **VIEWS** são queries salvas, ou seja, a gente cria uma query, da um nome para ela e escreve todo o script, depois quando quisermos usa-la novamente, ao invés de reescrever todo o script, nós apenas à chamamos. No exemplo abaixo eu estou fazendo um **SELECT** de algumas informações dos clientes:
```sql
SELECT
    cus.customer_id,
    cus.first_name,
    cus.last_name,
    pay.amount
FROM customer AS cus
JOIN payment AS pay
    ON cus.customer_id = pay.customer_id
```
Essa consulta me retorna as informações que eu pedi. Mas se essa consulta é uma query que eu vou precisar ficar repetindo varias vezes, eu posso transformar ela em uma **VIEW**, faço assim:
```sql
CREATE VIEW vendas_por_cliente AS
SELECT
    cus.customer_id,
    cus.first_name,
    cus.last_name,
    pay.amount
FROM customer AS cus
JOIN payment AS pay
    ON cus.customer_id = pay.customer_id
```
Assim, toda vez que eu precisar dos dados eu chamo a **VIEW**. Agora eu quero agora saber todos os clientes que o *"amount"* é maior ou igual a 9.99, como a **VIEW** já está criada, eu faço a condição chamando ela, eu faço assim:
```sql
SELECT *
FROM vendas_por_cliente
WHERE amount >= 9.99
```

# Realizando o *DROP* ou *REPLACE*:
- Para alterar uma **VIEW** que já existe, basta digitar na frente o **REPLACE**, assim:
```sql
CREATE OR REPLACE VIEW nome
CODIGO ABAIXO
.
.
.
```
Como boa prática de programação, sempre que for criar uma view, o melhor é já colocar o **REPLACE** junto, assim se já existe a view é alterada, se ainda não existe ela é criada.

- Para deletar uma **VIEW** basta digitar o **DROP**, assim:
```sql
DROP VIEW nome
```

# Funções com Strings:
Assim como existe funções para trabalhar com números, existem funções para trabalhar com strings. Podemos consultar várias funções no google, mas segue alguns exemplos abaixo:
- **TRIM**: essa é uma função bem legal, ela apaga todos os espaços que existem antes da primeira letra e depois da última letra. Ela não apaga os espaços do meio da string. Exemplo:
```sql
SELECT TRIM('   texto com espaço   ');
```
Vai me retornar **'texto com espaço'**.
- **LTRIM**: essa remove os espaços da esquerda:
```sql
SELECT LTRIM('    texto com espaço    ');
```
Vai me retornar **'texto com espaço '** (no markdown não da para colocar espaços, mas fica o exemplo).
- **RTRIM**: essa remove os espaços da direita:
```sql
SELECT RTRIM('    texto com espaço    ');
```
Vai me retornar **'    texto com espaço'**.
- **TRIM BOTH**: com ele você pode remover carácteres específicos do início e fim da string:
```sql
SELECT TRIM(BOTH 'a' FROM 'aaatextoaaa');
```
Vai me retornar **texto**.
- **TRIM LEADING**: remove o caracter apenas do início:
```sql
SELECT TRIM (LEADING 'a' FROM 'aaatextoaaa');
```
Vai me retornar **textoaaa**.
- **TRIM TRAILING**: remove o caracter apenas do final:
```sql
SELECT TRIM(TRAILING 'a' FROM 'aaatextoaaa');
```
Vai me retornar **aaatexto**.
- **LOCATE**: serve para localizar a posição de um caracter:
```sql
SELECT LOCATE('o', 'texto');
```
Vai me retornar: **5**.
- **LCASE**: altera toda a string para minúsculo:
```sql
SELECT LCASE('TEXTO');
```
Vai me retornar **texto**.
- **UCASE**: altera toda a string para maiúsculo:
```sql
SELECT UCASE('texto');
```
Vai me retornar **TEXTO**.
- **LENGTH**: conta quantos caracteres tem na string:
```sql
SELECT LENGTH('texto');
```
Vai me retornar **5**.
- **REPEAT**: repete a string o número de vezes colocado na condição:
```sql
SELECT REPEAT('texto', 4)
```
Vai me retornar **textotextotextotexto**.

# Criando um database:
Nessa etapa, eu irei criar um banco de dados do zero, com as tabelas e dados. No exemplo eu estou criando a database para uma concessionária de carros.
```sql
CREATE DATABASE carros;
```

# Criando a tabela de marcas:
Vams criar algumas tabelas, elas são:
- marcas,
- inventario,
- clientes

Para criar uma tabela, usamos:
```sql
CREATE TABLE marcas (
    id_marcas INT NOT NULL AUTO_INCREMENT,
    nome_marca VARCHAR(255) NOT NULL,
    PRIMARY KEY (id_marcas)
);
```

# Atualizando colunas dentro de uma tabela:
Em uma tabela, se quisermos alterar informações, ou até mesmo adicionar mais colunas, fazemos assim:
- Para adicionar uma nova coluna:
```sql
ALTER TABLE marcas ADD origem VARCHAR(255);
```
- Para alterar uma coluna que já existe:
```sql
ALTER TABLE marcas
MODIFY COLUMN origem VARCHAR(255) NOT NULL;
```
**Importante**: O *MODIFY* é no MySQL, vale consultar qual é o comando equivalente no seu banco.

# Criando a tabela de inventário:
Vamos criar a tabela *inventario* que será associada a tabela *marcas*:
```sql
CREATE TABLE inventario (
    id_inventario INT NOT NULL AUTO_INCREMENT,
    modelo VARCHAR(255) NOT NULL,
    transmissao VARCHAR(255) NOT NULL,
    motor VARCHAR(255) NOT NULL,
    combustivel VARCHAR(255) NOT NULL,
    id_marcas INT NOT NULL,
    PRIMARY KEY (id_inventario),
    FOREIGN KEY (id_marcas) REFERENCES marcas(id_marcas)
);
```
# Criando a tabela de clientes:
```sql
CREATE TABLE cliente (
    id_cliente INT NOT NULL AUTO_INCREMENT,
    nome VARCHAR(255) NOT NULL,
    sobrenome VARCHAR(255) NOT NULL,
    PRIMARY KEY (id_cliente)
);
```

# SQL *Data Types*:
São formatos de dados que atribuimos às colunas. Podemos consultar vários formatos no google para decidir o que seja mais adequado a cada coluna.

# Inserindo dados na tabela:
Primeiro ponto, para inserir dados em uma tabela, devemos respeitar a ordem das colunas. O campo de *id* se definios ele como *AUTO_INCREMENT* não precisamos inserir, pois ele é inserido sozinho.
```sql
INSERT INTO clientes(nome, sobrenome, endereco)
VALUES
    ('Jose', 'Mario', 'Rua 1'),
    ('Mario', 'Jose', 'Rua 2'),
    ('Maria', 'Joao', 'Rua 3'),
    ('Joao', 'Maria', 'Rua 4'),
    ('Jose', 'Silva', 'Rua 5');
```

# Completando a inserção de dados:
```sql
INSERT INTO marcas (nome_marca, origem)
VALUES
    ('BMW', 'Alemanha'),
    ('Fiat', 'Italia'),
    ('Mercedes-Benz', 'Alemanha'),
    ('Renault', 'Franca'),
    ('Jaguar', 'Inglaterra');
```

```sql
INSERT INTO inventario (modelo, transmissao, motor, combustivel, id_marcas)
VALUES
    ('320i',        'Automática', '2.0 Turbo', 'Gasolina', 1),
    ('Toro',        'Automática', '1.3 Turbo', 'Flex',     2),
    ('C 200',       'Automática', '1.5 Turbo', 'Gasolina', 3),
    ('Kwid',        'Manual',     '1.0',       'Flex',     4),
    ('F-Pace',      'Automática', '2.0 Turbo', 'Gasolina', 5);
```

# Visualizando a *DB* de usuários:
Isso é muito importante, porque cada usuário em um banco de dados deve ter o seu próprio *user* com as devidas permissões, por exemplo, permissão para ler, editar, excluir, ou visualizar algo, etc...
Para ver os usuários dentro do MySQL, fazemos:
```sql
USE mysql;
SELECT * FROM user;
```
# Criando um novo usuário:
Vamos criar 3 usuários:
- ruan,
- joao,
- maria

```sql
CREATE USER ruan IDENTIFIED BY 'SENHAAQUI';
```
**Importante**: essa senha é apenas de teste, em um ambiente real de produção a senha deve ser difícil e segura.
Nesse exemplo o *'ruan'* pode acessar o banco de qualquer lugar, pois não foi limitado o local de acesso. Vamos criar agora o *'joao'* e limitar o aesso dele:
```sql
CREATE USER joao@localhost IDENTIFIED BY 'SENHAAQUI';
```
Dessa forma o *'joao'* só poderá acessar o banco direto no servidor, ou seja, estando lá.
Agora vamos criar o usuário *'maria'*:
```sql
CREATE USER maria@empresa.com IDENTIFIED BY 'SENHAAQUI';
```
Nesse exemplo a *'maria'* só pode acessar o banco de um computador que esteja conectado ao domínio *'empresa.com'*, ou através de uma VPN.

# Removendo um usuário:
Para remover um usuário é bem simples, basta usar o *DROP*, mas temos que colocar o nome e de onde o usuário acessa, quando isso foi setado no banco. Exemplo, a usuária *'maria'* foi setado que ela iria usar o banco do domínio da empresa, então fazemos:
```sql
DROP USER maria@empresa.com;
```

# Recuperando a senha de um usuário:
Se algum usuário esquecer a senha, nós podemos altera-la passando o seguinte comando:
```sql
SET PASSWORD FOR joao@localhost = 'NOVASENHA';
```
**Importante**: como na criação foi setado que o *'joao'* só poderia acessar ao banco do localhost, para trocar sua senha, precisamos passar isso também.

# Aplicando privilégios a usuários:
Quando temos vários usuários e não queremos que todos eles tenham acesso total ao banco, ou à todas as tabelas, nós podemos aplicar determinados privilégios à eles.
Por padrão um novo usuário vem sem nenhuma permissão, então temos que defini-las. Primeiro precisamos ver as permissões atuais que uma pessoa tem, para isso:
```sql
SHOW GRANTS FOR joao@localhost;
```
Agora eu quero dar permissão para que o *'joao'* faça *SELECT*, *INSERT*, *UPDATE* e *DELETE* apenas no banco *sakila*, em todas as tabelas.
```sql
GRANT SELECT, INSERT, UPDATE, DELETE
ON sakila.*
TO joao@localhost;
```

# Adicionando um admin:
Se eu quiser que uma determinada pessoa tenha todos os privilégios em um determinado banco, eu transformo essa pessoa em admin, ou seja, ela vai poder fazer tudo no banco que eu setar à ela. Ou podemos também definir que uma pessoa seja admin de todo o MySQL.
- Para definir todos os privilégios para um determinado banco, fazemos:
```sql
GRANT ALL
ON sakila.*
To joao@localhost;
```
- Agora para definir que uma pessoa será admin de tudo, ou seja, de todo o servidor, fazemos:
```sql
GRANT ALL
ON *.*
TO ruan;
```
Dessa forma o usuário *'joao'* se tornou admin apenas do banco *sakila*, enquanto o usuário *'ruan'* se tornou admin de todo o servidor.

# Removendo privilégios:
Vamos usar de exemplo que queremos remover as permissões de um usuário, deixando ele apenas com permissão para *SELECT* e *INSERT*, no exemplo o usuário tem permissão para *SELECT*, *INSERT* e *UPDATE*, queremos remover o *UPDATE*. Fazemos:
```sql
REVOKE UPDATE
ON sakila.*
FROM usuario;
```
Com isso o usuário terá permissão apenas para *SELECT* e *INSERT*.

Curso: SQL DO ZERO AO AVANÇADO.
PROFESSOR: ANDRÉ IACONO
LINK: https://www.udemy.com/course/curso-sql-do-zero-ao-avancado/

# FIM DO CURSO!!