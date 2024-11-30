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
SELECT <lista atributos>
FROM  <tabelas desejadas>
(WHERE <condições>) 
(ORDER BY <lista atributos>)

Onde *SELECT* seleciona todos os alguns atributos desejados, *FROM* seleciona as tabelas que farão parte da resposta da consulta, *WHERE* indica as condições que cada tupla deve ter para aparecer na consulta e *ORDER BY* ordena a consulta por ordem de inserção de atributo.
