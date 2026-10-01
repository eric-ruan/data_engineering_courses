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
WHERE actor_id
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
WHERE amount BETWEEN 0.99 AND 3.00
```
Dessa forma a consulta vai me retornar valores que são *>=* à 0.99 e *<=*, esse operador ajuda a deixar os códigos mais limpos, ao invés de usar o *AND* para tudo.

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
WHERE nome REGEXP '^[aeiou]$'
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