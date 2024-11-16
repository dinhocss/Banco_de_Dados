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
  Pnome VARCHAR(15) NOT NULL,
  Unome VARCHAR(15) NOT NULL,
  Cpf CHAR(11) NOT NULL,
  Datanasc DATE,
  Endereco VARCHAR(30),
  Cpf_supervisor CHAR(11) NOT NULL,
  PRIMAREY KEY(Cpf),
  FOREIGN KEY(Cpf_supervisor) REFERENCES FUNCIONARIO(Cpf)
);
```

