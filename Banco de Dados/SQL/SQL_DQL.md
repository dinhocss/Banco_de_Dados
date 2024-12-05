> É um subconjunto de comandos utilizado para consultar dados em um banco de dados.

## Consultas de alteração básicas em SQL

A operação básica de consulta em SQL é a palavra-chave *SELECT*. Junto com outros termos, ela fornece um poderoso meio de visualização de dados, podendo combinar duas ou mais tabelas para uma melhor visualização.
Além de *SELECT*, também podemos utilizar *FROM* e *WHERE*. Juntos, eles formam a estrutura básica para consultas em SQL.

### A estrutura SELECT-FROM-WHERE

Para realizarmos as operações de busca de dados precisamos utilizar a seguinte estrutura:

```
SELECT <lista de atributos>
FROM <tabelas desejadas>
WHERE <condição> 
```

Onde a lista de atributos são os atributos que serão recuperados, as tabelas desejadas são listadas e separadas por vírgula, e a condição geralmente é onde atribuimos as chaves das tabelas que possuem um relacionamento, e onde definimos condições específicas. Por exemplo, suponhamos que desejamos buscar no banco de dados um funcionário chamado João Carlos. Podemos realizar a consulta da seguinte maneira:

```
SELECT nome, dataNasc, idade
FROM funcionario
WHERE nome = 'João Carlos'
```

A clausula *WHERE* é equivalente a seleção de álgebra relacional. Isso por que ela seleciona tuplas que satisfazem a condição desejada. Já a clausula *SELECT* pode ser comparada com uma projeção, onde os atributos desejados são projetados da tabela.

**OBS**: Se quisermos selecionar todos os atributos de uma tabela, utilizamos `SELECT *`.

Podemos utilizar os operadores booleanos AND, OR e NOT para compararmos mais de uma condição. Por exemplo, suponhamos que a gente deseje obter informações sobre funcionários que trabalham no departamento de pesquisa. Um exemplo é dado abaixo:

```
SELECT nome, sobrenome, dep
FROM funcionario, departamento
WHERE funcionario.idDep = departamento.idDep AND departamento.nomeDep = 'Pesquisa'
```

departamento.nomeDep = 'Pesquisa' é chamada condição de seleção, pois selecionamos as tuplas na qual nomeDep seja 'Pesquisa'. Já funcionario.idDep = departamento.idDep é uma condição de junção, pois essa condição é responsável por atribuir cada funcionário com cada departamento.

### Nomes de atributos ambíguos, apelidos, renomeação de atributos

Dois atributos iguais podem ser exibidos em uma visualização da tabela, porém, isto só ocorre se os atributos forem de tabelas diferentes. Para declararmos atributos que possuam o mesmo nome precisamos colocar o nome da tabela da qual o atributo veio. Por exemplo:

```
SELECT funcionario.nome, departamento.nome
FROM funcionario, departamento
WHERE funcionario.depID = departamento.depID
```

Uma outra situação ocorre quando tentamos visualizar dados de duas tabelas iguais. Por exemplo, suponhamos que a gente deseje obter nome e sobrenome dos funcionários e de seus supervisores. Precisamos utilizar a mesma tabela duas vezes, com isso, precisamos renomear os atributos para que não haja redundância. A renomeação é feita através da palavra-chave *AS*. Exemplo:

```
SELECT E.nome AS Empregado, S.nome AS Supervisor
FROM funcionario AS E, funcionario AS S
WHERE E.Cpf_supervisor = S.Cpf 
```

**OBS**: A clausula *WHERE* não é obrigatória. Quando ela não é especificada, todas as tuplas da tabela serão exibidas. Caso tenha mais de uma tabela o resultado será o produto cartesiano das duas tabelas envolvidas.

### Tabelas como conjuntos em SQL

A linguagem SQL não elimina automaticamente tuplas repetidas no resultado de uma consulta. Para exibirmos uma consulta sem levar em consideração as tuplas repetidas utilizamos a palavra-chave *DISTINCT*. Esse comando irá eliminar qualquer duplicata na resposta da consulta. Por exemplo, para exibirmos apenas os dados diferentes de uma tabela fazemos:

```
SELECT DISTINCT pnome, unome
FROM funcionario
```

O SQL trata tabelas como conjuntos, por consequência, algumas operações sobre conjuntos podem ser utilizadas. Como por exemplo, operações de união (UNION), diferença (EXCEPT) e intersecção (INTERSECT), podem ser aplicadas sobre conjuntos. Uma restrição é que para que a operação funcione, as duas tabelas devem ser equivalentes, ou seja, possuirem o mesmo número de atributos e os atributos devem ter tipos compatíveis entre si. Segue um exemplo da união de dois conjuntos:

```
(SELECT DISTINCT ProjNumero
  FROM funcionario AS f, projeto AS p, departamento AS d
  WHERE p.depID = d.depID AND f.Cpf_gerente = f.Cpf AND Unome = 'Silva')
UNION
(SELECT DISTINCT ProjNumero
  FROM funcionario AS f, projeto AS p, trabalha_em AS t
  WHERE p.depID = t.depID AND f.cpf = t.cpf AND unome = 'Silva')
```

Observe como os atributos além de terem a mesma quantidade, também possuem o mesmo tipo. Isso é essencial para trabalhar com operações sobre conjuntos. No caso acima será selecionado a união entre *os gerentes que possuem o sobrenome Silva* e os *funcionarios que possuem o sobrenome Silva*.

### Combinação de padrão de subcadeias e operadores aritméticos

Podemos definir uma busca de uma subcadeia através da palavra-chave *LIKE*. A combinação de LIKE com '%' e '_' possibilita a busca de qualquer substring. Por exemplo, se precisamos saber o nome de todos os funcionários que começam com Jo, faremos a seguinte consulta:

```
SELECT nome
FROM funcionario
WHERE nome LIKE 'Jo%'
```

O símbolo % após Jo indica que o nome desejado começa com Jo e pode ter qualquer sufixo. Caso % estivesse antes de Jo, a busca retornaria os nomes que terminam com jo. % significa que pode ter diversos caractéres antes ou depois da substring desejada. Já '_' indica que apenas um caractére é substituido. Por exemplo, suponhamos que a gente deseje buscar os cpfs que terminem com 1:

```
SELECT cpf
FROM funcionario
WHERE cpf LIKE '_ _ _ _ _ _ _ 1'
```

Podemos utilizar operadores aritméricos em consultas. Para isso, o tipo do atributo deve ser um valor numérico. Por exemplo, se desejamos pesquisar os efeitos que um aumento de 10% do salário proporciona, podemos fazer a seguinte consulta:

```
SELECT F.pnome, F.unome, 1.1*F.salario AS aumento_salario
FROM funcionario F, projeto P, trabalha_em T
WHERE F.FuncID = T.FuncID AND P.projID = T.projID
```

### Ordem dos resultados da consulta

Para ordenarmos alguma consulta utilizamos a palavra-chave *ORDER BY*. Podemos adicionar diversos atributos, onde a prioridade dada a cada atributo é a ordem de inserção. Por exemplo, se quisermos imprimir nomes e sobrenomes dos funcionários de uma empresa, podemos ordená-los por ordem alfabética. Se colocarmos pnome seguido de unome, primeiramente será ordenada pelo nome, se houver nomes iguais, será ordenada pelo sobrenome. Segue abaixo um exemplo de como utilizar ORDER BY:

```
SELECT pnome, unome
FROM funcionarios
ORDER BY pnome, unome
```

**OBS**: Para definirmos uma ordem decrescente nós precisamos utilizar a palavra-chave DESC após o nome das condições de ordenação.

### Resumo das consultas de recuperação de SQL Básica

Uma consulta simples em SQL pode conter até quatro clausulas, mas apenas duas são obrigatórias. Segue abaixo a estrutura de uma consulta básica:

```
SELECT <lista atributos>
FROM  <tabelas desejadas>
(WHERE <condições>) 
(ORDER BY <lista atributos>)
```

Onde *SELECT* seleciona todos os alguns atributos desejados, *FROM* seleciona as tabelas que farão parte da resposta da consulta, *WHERE* indica as condições que cada tupla deve ter para aparecer na consulta e *ORDER BY* ordena a consulta por ordem de inserção de atributo.

## Consultas de alteração complexas em SQL

### Comparação envolvendo valores NULL

Em SQL os valores NULL dos atributos são diferentes entre si, sendo assim, não é possível fazer comparação entre valores do tipo NULL em SQL. Para isso, precisamos utilizar a palavra-chave *IS* ou *IS NOT* para verificar se há ou não a presença de um valor NULL. 

Por exemplo, suponha que se deseje consultar os funcionários que não possuem supervisor, então a consulta poderia ser a seguinte:

```
SELECT Pnome, Unome
FROM funcionario
WHERE Cpf_supervisor IS NULL;
```

### Consultas aninhadas

> São blocos select-from-where utilizados dentro de uma clausula WHERE

As consultas aninhadas são uma forma alternativa de se realizar consultas, podendo aninhar quantos blocos select-from-where forem necessários. Em uma consulta aninhada temos a tabela externa que terá um atributo que será utilizado como comparação para a tabela da subconsulta. Por exemplo, observe a consulta abaixo:

```
SELECT o.AirportCode as Origem
FROM airport AS o
WHERE o.AirportID IN (
	SELECT r.from
	FROM route as r
)
```

Na consulta acima, selecionamos o código do aeroporto da tabela *airport*, em seguida utilizamos o atributo *AirportID* como comparação. Ao utilizarmos *IN*, nosso atributo será comparado com o resultado da subconsulta, que nesse caso são todos os aeroportos de origem de uma determinada rota. Esse valor será comparado com o valor da subconsulta e retornará true se forem iguais, entrando na visualização final da tabela. 

#### Operadores ANY e ALL

São operadores que possibilitam utilizar operadores lógicos junto a consulta. Por exemplo, a consulta feita acima pode ser reescrita utilizando o operador *ANY* ao invés de *IN*, junto com um operador lógico, fazendo com que a consulta seja da seguinte maneira:

```
SELECT o.AirportCode as Origem, d.AirportCode as Destino
FROM airport AS o, airport AS d
WHERE (o.AirportID, d.AirportID) = ANY (
	SELECT r.from, r.to
	FROM route AS r
)
```

O operador *ANY* irá retornar qualquer ocorrência que satisfaça a condição dada. No caso acima a condição é que o.AirportID e d.AirportID precisam ser iguais a QUALQUER r.from, r.to. Ou seja, caso a gente tenha uma rota onde r.from = o.AirportID e r.to = d.AirportID, o resultado será exibido na consulta final. 

No caso de *ALL* todos os valores devem satisfazer a condição dada. Por exemplo, caso a gente queira verificar quais funcionários recebem mais do que um departamento qualquer podemos fazer a seguinte consulta:

```
SELECT Pnome, Unome
FROM funcionario
WHERE salario > ALL(
	SELECT salario
	FROM funcionario
	WHERE codDep = 5
)
```

**OBS:** É uma boa prática renomear tabelas e atributos para uma melhor manutenção do código e facilidade de leitura

#### Operador EXISTS/NOT EXISTS

O operador *EXISTS* serve para verificar se uma determinada ocorrência é válida na consulta, caso seja válida ela retorna para o resultado final. Por exemplo, suponhamos a seguinte consulta:

```
SELECT o.AirportCode as Origem, d.AirportCode as Destino
FROM airport AS o, airport AS d
WHERE EXISTS (
	SELECT r.from, r.to
	FROM route AS r
	WHERE r.from = o.AirportID AND r.to = d.AirportID
)
```

De maneira similar, o *NOT EXISTS* verifica se uma subconsulta não possui nenhuma correspondência. Por exemplo, imagina que  a gente queira verificar os funcionários que não estão relacionados a nenhum projeto, então a consulta pode ser do tipo:

```
SELECT Pnome, Unome
FROM funcionario as f
WHERE NOT EXISTS(
	SELECT *
	FROM projeto as p
	WHERE p.funcionarioID = f.funcionarioID
)
```

A subconsulta acima retorna todos os funcionários que possuem vínculo com algum projeto. A consulta externa irá comparar cada funcionário com essa lista de funcionários com projeto. Se o funcionário f em questão não estiver na lista da subconsulta, então ele não está vinculado a nenhum projeto. 

### Tabelas de Junção e junções externas (OUTER)

O conceito de tabela de junção é utilizado para podermos relacionar duas tabelas, porém sem precisar necessariamente que as condições de atribuição e de seleção estejam na mesma clausula WHERE. As tabelas de junção permitem que o código seja mais legível, pois permite a separação de condições. 

Podemos ter diferentes tipos de junção, sendo elas:

#### NATURAL JOIN

É um tipo de junção no qual não é necessário especificar a condição de junção. A junção será feita com base em nomes equivalentes de atributos, que serão comparados, fornecendo o produto cartesiano das tabelas envolvidas.

Por exemplo: 
```
SELECT o.AirportCode as Origem, d.AirportCode as Destino, r.RouteID as Rota
FROM (airport AS o,airport AS d) NATURAL JOIN route AS r
ORDER BY o.AirportCode, d.AirportCode
```

Na consulta acima será retornada uma tabela referente ao produto cartesiano entre as tabelas o, d e r.

#### INNER JOIN (ou JOIN)

Utilizada para relacionar duas ou mais tabelas através de suas chaves primaria e estrangeira. Utiliza-se a clausula *ON* para especificar a condição de junção, permitindo que ela esteja separada da condição de seleção.

```
SELECT r.RouteID AS Rota,o.AirportCode AS Origem, d.AirportCode AS Destino
FROM (airport AS o, airport AS d) JOIN route AS r ON (r.from = o.AirportID AND r.to = d.AirportID)
ORDER BY o.AirportCode, d.AirportCode
```

Observe que no exemplo acima utilizamos 3 tabelas, que se relacionam através das chaves r.from = o.airportID e r.to = d.airportID. A clausula JOIN permite um grande número de possibilidades, enquanto torna o código mais fácil de ler. 

#### OUTER JOIN

Permite que se consulte todos os registros de uma ou ambas as tabelas, mesmo quando não existe correspondência. O valor retornado será NULL para atributos que não possuam uma correspondência. 

Podemos ter três tipos de junção externa, sendo elas:

##### LEFT OUTER JOIN

Permite que a consulta retorne todos os elementos da tabela esquerda, e seus correspondentes da direita. Caso seu correspondente não exista um valor NULL será retornado. 

Exemplo:

```
SELECT o.AirportCode, r.RouteID, o.AirportID
FROM airport AS o LEFT OUTER JOIN route AS r ON (r.from = o.AirportID)
```

A consulta acima pega todas as correspondências de airport e exibe junto com seus correspondentes em route. Caso haja algum routeID que não esteja relacionado a nenhum AirportID, será retornado NULL.

##### RIGHT OUTER JOIN

Semelhante ao *LEFT JOIN* porém exibe a tabela da direita completamente, junto com seus correspondentes da esquerda. Da mesma forma, caso não haja correspondente a esquerda, um valor NULL será retornado. Por exemplo:

```
SELECT o.AirportCode, r.RouteID, o.AirportID
FROM airport AS o RIGHT OUTER JOIN route AS r ON (r.from = o.AirportID)
```

No caso acima, todos os registros de route serão exibidos, junto com seus correspondentes. Não haverá valores nulos, pois para existir uma rota precisa existir um código de aeroporto e um ID referente ao aerporto, fazendo com que sempre haja valores presentes.

##### FULL OUTER JOIN

Exibe todos os registros de ambas as tabelas, retornando NULO para tabelas que não possuam nenhuma associação. Por exemplo:

```
SELECT AirportCode, RouteID, AirportID
FROM airport FULL JOIN route ON route.from = AirportID
```

### Funções de Agregação em SQL

> São utilizadas para resumir informação de várias tuplas em uma única tupla.

Além das funções de agregação, temos também o agrupamento, que permite agrupar tuplas baseadas em uma lógica pré-definida. Existem diversas funções de agregação já embutidas em SQL, sendo elas: *COUNT*, *SUM*, *MAX*, *MIN* e *AVG*

As funções *SUM*,*MAX*,*MIN* e *AVG* são utilizadas em cima de valores numéricos e retorna, respectivamente, a soma, o valor máximo, o valor mínimo e a média dos valores utilizados durante a consulta.

**OBS**: Os valores de *MAX* e *MIN* podem ser aplicados a valores não numéricos, contanto que haja uma ordem entre esses valores.

Por exemplo, suponha a consulta que retorne a maior distância entre os aeroportos, a menor distância, a média entre as distâncias e a soma entre as distâncias. Poderíamos realizar essa consulta da seguinte maneira:

```
SELECT MAX(Distance), MIN(Distance), AVG(Distance), SUM(Distance)
FROM route
```

Note que cada atributo da consulta deverá ser apenas um valor, portanto todos os atributos devem ser compatíveis. 

Já a função *COUNT* é utilizada para contar quantos registros a tabela possui. Podendo fornecer a quantidade total de registros, ou apenas registros que satisfaçam alguma condição. Por exemplo:

```
SELECT COUNT(*)
FROM airport JOIN route ON (airportID = route.from)
```

### GROUP BY e HAVING

Utilizamos a clausula GROUP BY quando queremos aplicar funções de agregação a subgrupos de tuplas. Por exemplo, através de GROUP BY podemos calcular o número de funcionários presente em cada departamento, ou a média de salário dos funcionários de cada departamento. Portanto, quando utilizamos funções de agregação, devemos utilizar GROUP BY caso a gente não queira que a função de agregação aja sobre todas as tuplas da tabela.

GROUP BY especifica os atributos de agrupamento, e esses atributos devem, obrigatoriamente, aparecer na clausula SELECT. Portanto, tudo que estiver em SELECT, deve também estar em GROUP BY. 

Por exemplo, imagine que se deseja saber a quantidade média de assentos agrupada por vôo, mas apenas para vôos com quantidade média de assentos maior do que 50, então a consulta poderia ser feita da seguinte maneira:

```
SELECT AVG(f.MaxSeats)
FROM class AS c JOIN flightclass AS f ON (c.FlightID = f.FlightID)
GROUP BY f.FlightID
HAVING AVG(f.MaxSeats) > 50
```

No exemplo acima selecionamos a média de assentos da tabela class. O GROUP BY irá agrupar os vôos diferentes, e cada tupla de flight terá sua média de assentos. Em seguida, utilizamos o HAVING para pegar apenas as tuplas na qual a média de assentos é maior que 50. 

**OBS:** Se houver NULLS no atributo de agrupamento, então um grupo separado é criado para todas as tuplas com o valor NULL.

A clausula HAVING oferece uma condição em cima do grupo de tuplas retornado pela clausula GROUP BY, fazendo com que somente os grupos que satisfazem a condição serão retornados para consulta. Por exemplo, imagine que desejemos selecionar a quantidade de funcionários que trabalham em um determinado projeto, porém queremos apenas projetos que possuam 2 ou mais funcionários, então a consulta poderia ser:

```
SELECT Projnumero, Projnome, COUNT(*)
FROM Projeto AS p JOIN Trabalha_Em AS t ON (Projnumero = Pnr)
GROUP BY Projnumero, Projnome
HAVING COUNT(*) > 2
```

**OBS:** A clausula WHERE filtra tuplas ANTES da agregação, enquanto a clausula HAVING filtra grupos APÓS a agregação

### Resumo das consultas

Uma consulta em SQL pode ter até seis clausulas, mas comente *SELECT* e *FROM* são obrigatórias. Segue abaixo um resumo de como uma consulta é feita:

**SELECT** <lista de atributos e função>
**FROM** <'lista tabela'>
(**WHERE**  <condição>)
(**GROUP BY** <'atributos de agrupamento'>)
( **HAVING**  <condição de grupo>)
(**ORDER BY** <'lista atributos'>);

Temos também as funções de agregação **COUNT**, **SUM**, **MIN**, **MAX** e **AVG**.

Utilizamos **IN** e **NOT IN** junto com a clausula **WHERE** para representar consultas aninhadas. Um exemplo da utilização de **IN** é dado abaixo, onde desejamos selecionar o código do aeroporto de desino e origem da rota que possui a menor duração:

```
SELECT o.AirportCode as Origem, d.AirportCode as Destino
FROM (airport AS o JOIN route AS r ON r.from = o.AirportID) JOIN airport AS d ON r.to = d.AirportID
WHERE r.Duration IN (
	SELECT MIN(r2.Duration)
	FROM route AS r2
)
```



