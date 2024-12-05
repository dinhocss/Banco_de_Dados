
 # Instruções *INSERT*, *DELETE* e *UPDATE* em SQL

Em SQL, utilizamos as clausulas *INSERT*, *DELETE* e *UPDATE* para adicionarmos, atualizarmos e removermos dados de um banco de dados. 

## O comando *INSERT*

> *INSERT* é utilizado para adicionar uma única tupla em uma tabela.

Para adicionarmos valores a uma tabela precisamos especificar o nome da tabela que se deseja adicionar a tupla, junto com os valores de atributos **na mesma ordem** que foi definido ao criarmos a tabela. Por exemplo, vejamos como criar um funcionario. Primeiramente devemos verificar como a ordem da tabela foi definida.  A tabela é dada a seguir:

```
CREATE TABLE EMPREGADO (
NOME VARCHAR(15) NOT NULL,
INICIALM CHAR,
SOBRENOME VARCHAR(15) NOT NULL,
CPF VARCHAR(11) NOT NULL,
DNASCIMENTO DATE,
ENDERECO VARCHAR(30),
SEXO CHAR,
SALARIO FLOAT,
CPF_SUPERVISOR VARCHAR(11),
COD_DEPTO INT NOT NULL,
PRIMARY KEY(CPF),
FOREIGN KEY (CPF_SUPERVISOR) REFERENCES EMPREGADO (CPF),
FOREIGN KEY (COD_DEPTO) REFERENCES DEPARTAMENTO (COD_DEPTO));
```

Com isso, para inserção de um novo empregado, precisamos utilizar o seguinte código:

```
INSERT INTO EMPREGADO 
VALUES('Ricardo','P','Lonnev','13313234311', '1954-10-30', 'Rua epifania moura, 32', 'M',32.400,'13313234311',1)
```

Uma outra forma de inserirmos registros em uma tabela é especificando explicitamente os atributos no qual se deseja adicionar. Podemos não adicionar nenhum valor em atributos que não possuam a clausula *NOT NULL*. Portanto, para adicionarmos um empregado no qual a gente só sabe o primeiro nome, ultimo nome, cpf, por exemplo:

```
INSERT INTO EMPREGADO (NOME, SOBRENOME, CPF, COD_DEPTO)
VALUES('Priscilla','Veigar','200293192',2)
```

**OBS**: Todos os valores que não forem especificados terão valor NULL ou DEFAULT. 

## O comando *DELETE*

> Remove tuplas de uma tabela

Utilizamos a clausula WHERE para especificarmos qual tupla será removida. Dependendo das restrições de integridade definidas na DDL, uma mesma clausula *DELETE* pode remover zero ou mais tuplas em uma tabela. As restrições de integridade nesse caso são utilizadas nas definições de chave estrangeira, onde podemos definir *ON DELETE SET NULL*, *ON DELETE SET DEFAULT*, *ON DELETE CASCADE*, entre outros. 

Segue abaixo um exemplo de como utilizar *DELETE* para removermos tuplas de uma tabela:

```
DELETE FROM departamento
WHERE COD_DEPTO = 2
```

Quando removermos alguma tupla precisamos garantir que o valor que passamos na clausula *WHERE* não possua nenhuma restrição de integridade. Por exemplo, caso em COD_DEPTO não houvesse informações na definição da tabela a respeito da exclusão desse atributo, então o SGDB, por padrão, não iria remover a tupla. Para isso, precisamos definir um ON DELETE para especificar como lidar com a exclusão de uma tupla que está sendo referenciada por outra tupla.

## O comando UPDATE

>Altera o valor de uma ou mais tuplas de uma tabela do banco de dados

Assim como no comando *DELETE*, o comando *UPDATE* também utiliza uma clausula *WHERE* para definir o atributo a ser modificado. Uma clausula *SET* define o atributo a ser modificado e seu novo valor. Por exemplo, caso a gente queira adicionar um valor ao atributo CPF_GERENTE, podemos fazer:

```
UPDATE empregado
SET CPF_GERENTE = '12183284790'
WHERE CPF = '20093849931'
```

Podemos também modificar valores numéricos ao realizar operações matemáticas sobre eles. Por exemplo, caso a gente queira modificar o salário de todo um departamento, podemos usar as seguintes operações:

```
UPDATE empregado
SET SALARIO = SALARIO + (SALARIO*0.1)
WHERE COD_DEPTO = 3
```
