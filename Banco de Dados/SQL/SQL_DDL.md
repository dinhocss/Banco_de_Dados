>O SQL é conhecido hoje como Structured Query Language, e é uma linguagem padrão utilizada por SGBDs relacionais.

A linguagem SQL é a principal ferramenta para interagir com um banco de dados relacional. Ela permite criar, consultar e deletar dados de maneira eficiente. O SQL pode ser subdividido em diversas subcategorias, sendo elas:
- **DDL(Data Definition Language):** Utilizada para definir a estrutura do banco de dados e seus objetos. Comandos como `CREATE`, `DROP`, `ALTER` e `TRUNCATE` são utilizados.
- **DML(Data Manipulation Language):** Permite inserir, atualizar ou excluir dados na tabela. Exemplos: `INSERT`,`UPDATE`,`DELETE`.
- **DQL(Data Query Language):** Focada em consultas, utilizando o comando `SELECT`.
- **TCL(Transaction Control Language):** Controla transações, como os comandos `COMMIT` e `ROLLBACK`.

# Definições e Tipos de Dados em SQL

>O principal comando para definição de dados é o `CREATE`.

O comando `CREATE` pode ser usado para criar tabelas, esquemas e domínios. 

## Conceitos de esquema e catálogo em SQL

Um esquema pode ser definido como um 'container' que terá elementos de um mesmo tipo. Esses elementos podem ser tabelas, views, restrições, que descrevem o esquema criado ao utilzarmos o comando `CREATE SCHEMA`.Ao criarmos um schema precisamos definir o nome do schema e um identificador de autorização. Por exemplo:

```
CREATE SCHEMA financeiro AUTHORIZATION id_name;
```
**OBS:** Cada instrução em SQL termina com `;`

A ideia de catálogo em SQL é um 'container' que guarda um conjunto de schemas. Ao criarmos um catálogo, criamos também um INFORMATION_SCHEMA, que contém metadados referentes a todos os schemas disponíveis no catálogo. Podemos criar uma definição de domínio em um catálogo e os schemas poderão compartilhar essa definição entre si. Schemas também podem compartilhar restrições de integridade referencial somente se estiverem no mesmo catálogo.

## Tipos de dados de atributo e domínio em SQL

Precisamos levar em conta algumas características referentes ao comando `CREATE TABLE`. Como por exemplo, os atributos que são definidos em uma tabela possuem a mesma ordem em que são declarados. No entanto, as tuplas não são ordenadas dentro de uma relação.

Os tipos de dados básicos aceitos para atributos são numérico, cadeia ou sequencia de caracteres, cadeia ou sequencia de bit, booleano, data e hora.Segue abaixo uma breve explicação de cada tipo de dado:
- **Dados númericos:** Incluem números inteiros (INTEGER, INT e SMALLINT) e números de ponto flutuante(FLOAT, REAL e DOUBLE PRECISION).
- **Cadeia de caracteres:** São de tamanho fixo (CHAR(n) ou CHARACTER(n), onde n é o número máximo de caracteres) ou de tamanho variável (VARCHAR(n), CHAR VARYING(n) ou CHARACTER VARYING(n)).
- **Cadeia de bits:** Podem ser de tamanho fixo (BIT(n)) ou de tamanho variado (BIT VARYING(n)), onde n é o número máximo de bits.
- **Dados booleanos:** Aceitam valores TRUE ou FALSE.
- **Dados do tipo DATE e TIME**: São tipos de dados referentes a data e tempo. Seu formato é *YYYY-MM-DD* para DATE e *HH:MM:SS* para TIME. Restrições são aplicadas para verificar se a data adicionada é válida.
- **TIMESTAMP**: Inclui os campos DATE e TIME.

>Domínio é uma de definição de um tipo de dado que poderá ser utilizado em vários lugares dentro do banco de dados.

Utilizar dominios é uma boa prática, pois permite a reutilização do código e evita redundância. Porém, não é todo SGBD que possui esta implementação, como por exemplo, o MySQL que não possui o conceito de domínio. Podemos criar um domínio com a seguinte instrução:

```
CREATE DOMAIN TIPO_CPF AS CHAR(11)
```

***

# Especificando Restrições em SQL

Agora trataremos das restrições básicas que podem ser aplicadas em SQL como parte da criação de tabelas. Estas incluem restrições de chave e integridade referencial, entre outros. 

## Especificando restrições de atributo e defaults de atributo

Se quisermos um atributo com cardinalidade mínima obrigatória precisamos utilizar uma restrição `NOT NULL`, que define que os valores referentes aquele atributo não podem ser nulos. Isto é sempre especificado de maneira implicita para os atributos que fazem parte da chave primária da tabela. 

Um exemplo de construção de uma tabela em um banco de dados, com suas devidas restrições de integridade, são definidas abaixo:

```
CREATE TABLE FUNCIONARIO(
  Pnome VARCHAR(15) NOT NULL DEFAULT 'Desconhecido',
  Unome VARCHAR(15) NOT NULL,
  Idade INT NOT NULL CHECK(Idade>18),
  Cpf CHAR(11) NOT NULL,
  Datanasc DATE,
  Endereco VARCHAR(30),
  Cpf_supervisor CHAR(11) NOT NULL,
  PRIMAREY KEY(Cpf),
  FOREIGN KEY(Cpf_supervisor) REFERENCES FUNCIONARIO(Cpf)
);
```
Podemos também adicionar valores padrões através da palavra-chave *DEFAULT*, onde a cada nova tupla que não for informado um valor válido, o valor default será adicionado.
Uma outra restrição que pode ser aplicada sobre os atributos é CHECK. A restrição CHECK recebe como parâmetro uma condição a ser satisfeita para garantir a validade do dado. Caso o usuário tente adicionar um valor que não satisfaz a condição, a inserção não é feita. 

Em relação a integridade referencial, temos as chaves primárias e estrangeiras. Quando tivermos uma tabela com chave primária única, podemos declará-la diretamente no atributo. Por exemplo, a tabela FUNCIONARIO poderia ser escrita assim:

```
Cpf CHAR(11) NOT NULL PRIMARY KEY;
```

Quando criamos uma restrição de integridade um nome é gerado automaticamente. Porém, podemos explicitar um nome desejado, facilitando a manipulação e modificação dos dados referentes aquela restrição. Isso é feito através da palavra-chave *CONSTRAINT* e é utilizada da seguinte maneira:

```
idade INT NOT NULL CONSTRAINT chk_idade_minima CHECK (idade>18)
```

Para chaves estrangeiras utilizamos a restrição *FOREIGN KEY*, onde precisamos especificar, além do atributo que será a chave estrangeira, a tabela onde a chave primária está e o nome da chave primária. Junto da FOREIGN KEY podemos também definir ações para quando a chave primária que está sendo referenciada modificar seu valor, ou o registro for apagado. Para isso, podemos definir ações quando a chave primária é modificada (ON UPDATE) ou quando o registro da chave primária é removido (ON DELETE). Podemos ter opções como CASCADE, que atribui as modificações da chave primária na chave estrangeira, SET NULL, que define valor nulo caso a chave primária seja modificada ou removida, e SET DEFAULT, que define um valor default para quando a chave primária for modificada ou excluída. Segue um exemplo de como essas restrições são definidas:

```
FOREIGN KEY(Cpf_supervisor) REFERENCES Funcionario(Cpf)
ON DELETE SET NULL
ON UPDATE CASCADE
```
# Alteração de esquema

## O comando DROP

Utilizamos o comando DROP para excluir um esquema, tabela, restrições ou domínios. Existem duas opções de comportamentos para DROP, que são CASCADE e RESTRICT. Ao utilizarmos `DROP Funcionarios CASCADE`, nós excluímos a tabela Funcionarios, junto com todas suas tuplas e atributos. Ao utilizarmos RESTRICT no lugar de CASCADE, a tabela só será removida se não houver nenhuma referência a outras tabelas. Exemplo:

```
DROP SCHEMA Universidade CASCADE
DROP TABLE Funcionario RESTRICT
```

## O comando ALTER

Podemos utilizar o comando ALTER para modificar tabelas já existentes, como adição e remoção de colunas, alterar uma definição de coluna ou acrescentar ou remover restrições. Por exemplo, para adicionar colunas a tabelas já existentes podemos utilizar o seguinte comando:

```
ALTER TABLE universidade.funcionario ADD COLUMN Telefone VARCHAR(11);
```

Será acrescentado um atributo novo chamado Telefone na tabela *funcionario* no esquema *universidade*. Além disso, podemos alterar ou remover colunas. Segue abaixo um exemplo para cada caso:

```
ALTER TABLE universidade.funcionario ALTER COLUMN Cpf_supervisor SET DEFAULT '000000000';
ALTER TABLE universidade.funcionario DROP COLUMN Cpf_supervisor CASCADE;
```

Por último, podemos também modificar atributos já existentes utilizando *MODIFY COLUMN*. Por exemplo:

```
ALTER TABLE universidade.funcionario MODIFY COLUMN Idade INT NOT NULL;
```

**OBS**: Podemos adicionar restrições através de `ALTER TABLE fabrica.produto ADD CONSTRAINT chk_peso CHECK(Peso>50)`.
