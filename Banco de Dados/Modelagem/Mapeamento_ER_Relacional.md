# Transformações entre modelos

>O projeto lógico de um banco de dados relacional consiste em transformar o modelo ER conceitual em um modelo lógico, que implementa os dados abstratos no modelo ER

Um mesmo modelo conceitual pode gerar mais de um projeto lógico diferente, e apesar das informações serem iguais entre projetos lógicos diferentes, pode-se ter diferença na eficiência do banco de dados. Portanto, para um mapeamento mais efetivo, recomenda-se seguir um conjunto de regras. Estas regras possuem dois objetivos básicos:

- Obter um banco de dados que possua boa performance de consulta e alterações no banco de dados. Ou seja, o número de acessos a disco seja o menor possível.
- Obter um banco de dados que simplifique o desenvolvimento e manutenção de aplicações

Para alcançar os objetivos acima utilizamos um conjunto de regras recomendadas, que seguem os seguintes principios:

1. **Evitar junções - ter os dados necessários em uma única linha**
    - Quando precisamos realizar consultas em tabelas que possuam chave estrangeira o acesso ao disco é feito uma quantidade maior de vezes em relação a tabelas que possuam todas as informações em uma única linha. A operação para relacionar duas tabelas é a *JOIN*, que exige multiplos acessos ao disco.
2. **Diminuir o número de chaves primárias**
    - Para operações mais eficientes de manipulação de dados as chaves primárias utilizam a estrutura de índice. Essa estrutura consome um espaço considerável em disco, portanto é necessário que o número de chaves primárias seja o menor possível. As chaves primárias precisam garantir a unicidade de cada registro, sendo assim o número de chaves tem que ser o suficiente para essa garantia.
3. **Evitar campos opcionais**

A tradução do modelo ER para o modelo relacional é feito através dos seguintes passos:

1. Tradução inicial das entidades e seus respectivos atributos.
2. Tradução dos relacionamentos e seus respectivos atributos.
3. Tradução das generalizações/especializações.

## Implementação inicial de entidades

Neste passo, cada entidade será traduzida em uma tabela. Cada atributo da entidade será uma coluna da tabela. Os atributos identificadores da entidade correspondem a chave primária da tabela.

No exemplo abaixo a entidade Pessoa será transformada em uma tabela. Seus atributos serão as colunas da tabela e o código será a chave primária.

![image](https://github.com/user-attachments/assets/830a698a-42c4-4da3-b744-841467bd028a)

A transformação inicial resultaria no modelo relacional dado por: Pessoa(**CodPessoa**,Nome, Endereco, DataNasc, DataAdm).

### Nomes de atributos e nomes de colunas

Os nomes dados as colunas não precisam ser exatamente iguais aos dos atributos do modelo ER. É preferível que o nome das colunas sejam curtos para uma melhor eficiência do banco de dados. Na figura 1 temos alguns atributos como data de admissão, data de nascimento, que quando transformados no modelo relacional trocaram para dataNasc e dataAdm. 

**OBS:** Não é recomendado utilizar o nome da tabela no nome do atributo. Por exemplo, na Figura 1 o atributo nome não seria recomendado ser nomePessoa, pois ao referenciarmos esse atributo, utilizariamos Pessoa.nomePessoa. Com exceção da chave primária, que por ser referenciada em outras tabelas, ela precisa conter sua tabela de origem, como aconteceu com *codPessoa*.

Uma outra recomendação é em relação a abreviaturas. Geralmente, utilizamos abreviaturas em atributos que costumam a se repetir, e essas abreviaturas são iguais em todas as tabelas. Por exemplo, para código podemos utilizar cod, para números podemos utilizar num, etc.

### Relacionamento identificador

Quando temos um relacionamento identificador, ou seja, uma entidade fraca, a chave primária torna-se composta. Por exemplo, considere a figura abaixo:

![image](https://github.com/user-attachments/assets/5f5bd00b-a8dc-47aa-ba51-f8b46b1fab34)

A tabela dependente precisará de uma chave composta para poder ser identicada. Sempre que temos uma entidade fraca, esta entidade receberá em seu modelo relacional, a chave primária da entidade relacionada. Portanto, após o mapeamento teríamos: **Dependente(*CodEmp*,*NumSeq*, Nome).**

Podemos ter o caso no qual temos mais de uma entidade fraca relacionada. Por exemplo, a figura abaixo nos da um exemplo desse tipo:

![image](https://github.com/user-attachments/assets/4c9866c0-3ac3-409a-8d93-b22c290cf4d3)

Resultando no modelo relacional abaixo:

- **Grupo(*codGrupo*, nome)**
- **Empresa(*codGrupo*, *numEmp*, nome)**
- **Empregado(*codGrupo*,*numEmp*,*numEmpregado*, nome)**
- **Dependente(*codGrupo*,*numEmp*,*numEmpregado*,*numSeq*,nome)**

## Implementação de relacionamentos

>O fator determinante para a tradução a adotar no caso de relacionamentos é a cardinalidade mínima e a cardinalidade máxima.

Existem três formas básicas de se traduzir relacionamentos para o modelo relacional. Sendo elas:

### Tabela própria

Nesta tradução, o relacionamento é implementado através de uma tabela própria. Esta tabela contém as seguintes colunas:

- colunas correspondentes aos identificadores das entidades relacionadas
- colunas correspondentes aos atributos do relacionamento

A chave primária desta tabela é o conjunto dos identificadores das entidades relacionadas. Um exemplo deste tipo de tradução é mostrado abaixo:

![image](https://github.com/user-attachments/assets/b848645a-9a0d-4bbb-ba29-fd68f16134df)

O esquema relacional correspondente ao modelo acima é:

- Engenheiro(**codEng**,nome)
- Projeto(**codProj**,titulo)
- Atuacao(**codEng**,codProj,Funcao)
    - **codEng** referencia Engenheiro
    - **codProj** referencia Projeto

### Colunas adicionais dentro da tabela de entidade

>Esta tradução só é possível quando uma das entidades do relacionamento possui cardinalidade máxima um.

A tradução consta em inserir na tabela correspondente à entidade de cardinalidade máxima um, as seguintes colunas:

- Colunas correspondentes ao identificador da coluna relacionada; estas colunas serão chaves estrangeiras em relação a tabela que representa a chave referenciada.
- Colunas correspondentes aos atributos do relacionamento.

Segue abaixo um exemplo de como é feito o mapeamento para o modelo relacional empregando esses relacionamentos:

![image](https://github.com/user-attachments/assets/8a59a0a0-0c1a-4701-b5a6-7bbba041cd5b)

No caso da figura 5, temos a entidade empregado possuindo cardinalidade máxima 1 e a entidade Departamento possuindo cardinalidade máxima n. O mapeamento é feito adicionando na tabela EMPREGADO, o código do departamento e o atributo do relacionamento LOTACAO. Portanto, o esquema relacional correspondente seria:

- DEPARTAMENTO(**codDept**,nome)
- EMPREGADO(**codEmp**, nome, codDept, DataLot)
    - **codDept** referencia DEPARTAMENTO

### Fusão de tabelas de entidades

>Esta tradução pode ser aplicada quando o relacionamento entre as entidades for 1:1.

A tradução consta em juntar todos os atributos das duas tabelas relacionadas, bem como os atributos do relacionamento, em uma única tabela. Segue abaixo um exemplo de um modelo conceitual com relacionamento 1:1:

![image](https://github.com/user-attachments/assets/799914b1-f01f-496a-8975-58eb4fb37425)

No caso da figura 6, cria-se uma tabela que terá todos os atributos das entidades e dos relacionamentos. Portanto, o esquema relacional correspondente seria:

- CONFERENCIA(**codConf**, Nome, EndComissao, DataInst)

## Detalhes da implementação de relacionamentos
