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

Segue abaixo um resumo de qual tradução deve ser utilizada baseada em cada tipo de relacionamento:

![image](https://github.com/user-attachments/assets/1f6e2127-bb22-4227-823b-f64aa10d5fc0)

Para cada opção de relacionamento nós temos opções diferentes de implementação. Vamos detalhar cada caso, bem como qual é a tradução adequada para cada caso.

### Relacionamento 1:1

#### Ambas as entidades possuem participação opcional

A figura 8 apresenta um exemplo de um relacionamento 1:1, no qual a participação de ambas as entidades é opcional (cardinalidade mínima é zero). De acordo com a tabela apresentada na figura 7, a regra de implementação recomendada é a de Adição de Colunas, o que significa que precisamos atribuir os atributos do relacionamento, bem como uma chave estrangeira relacionando a entidade na qual ele está relacionado. 

![image](https://github.com/user-attachments/assets/3158fc0a-f1fd-48c2-bc6d-c0407f0bc5b2)

A implementação relacional seria:

- **HOMEM (IdentidadeHomem, nome)**
- **MULHER**(**IdentidadeMulher**,**nome, IdentidadeHomem, DataCasamento, RegimeCasamento)**
    - **IdentidadeHomem referencia HOMEM**
 
#### Uma entidade que tem participação opcional e outra que tem participação obrigatória

Um segundo caso pode ocorrer em um relacionamento 1:1, que é quando uma das entidades é obrigatória, enquanto a outra é opcional. Um exemplo dessa situação é exemplificada na figura abaixo:

![image](https://github.com/user-attachments/assets/f1207077-20c9-4982-8816-b883f6b070d0)

Neste caso, a tradução preferida é a de fusão de tabelas, resultando no seguinte esquema:

- **Correntista(codCorrentista, codCartao, Nome, DataExp)**

#### As duas entidades são obrigatórias

Por último, temos o caso onde as duas entidades são obrigatórias num relacionamento. Quando isto ocorre, a tradução indicada é a de fusão de tabelas. Considere a imagem abaixo:

![image](https://github.com/user-attachments/assets/7174824c-141a-4503-8e43-47fa20fa258b)

Neste último cso estamos lidando com entidades obrigatórias. De acordo com o resumo mostrado anteriormente, o esquema resultante é proveniente da fusão das tabelas acima. Note que os atributos do relacionamento também entram como atributos da tabela.

- **Conferencia(CodConf, Nome, DataInst, Ender)**

### Relacionamento 1:n

>No caso de relacionamentos 1:n a tradução preferível em qualquer um dos casos possíveis é a adição de colunas

A figura abaixo mostra um relacionamento 1:n, onde a cardinalidade mínima de ambas as entidades é 1 (obrigatória) e a cardinalidade máxima é 1:n. 

![image](https://github.com/user-attachments/assets/4be90c3f-1610-4b54-9c07-ecbe61cdf72e)

A tradução recomendada é a adição de colunas, onde os atributos dos relacionamentos e a chave primária da entidade relacionada será adicionada como atributo na tabela que possui cardinalidade máxima n. Sendo assim, o esquema relacional seria:

- **EDIFICIO(CodEd, Endereco)**
- **APARTAMENTO(NumApt,CodEd,Area)**
    - **CodEd referencia EDIFICIO**
 
Um outro exemplo é mostrado na figura abaixo. Neste caso, temos um relacionamento entre duas entidades opcionais.

![image](https://github.com/user-attachments/assets/689b1d15-7dfd-4c4f-ad33-cbf4ef378d0e)

Aqui a tradução recomendada também é a adição de coluna. A entidade que possui cardinalidade máxima n receberá a chave primária da entidade de cardinalidade máxima 1, assim como os atributos referentes ao relacionamento. Portanto, o esquema relacional ficaria o seguinte:

- **FINANCEIRA(CodFin, Nome)**
- **VENDA(idVenda,DataVenda,CodFin,NumPar,TaxaJuros)**
    - **CodFin referencia FINANCEIRA**
 
### Relacionamentos n:n

>Independente da cardinalidade mínima, relacionamentos n:n são sempre implementados via tabela própria

Sempre que tivermos duas entidades em que seus relacionamentos sejam n:n, nós utilizaremos a tradução de tabela própria. A nova tabela receberá as chaves primárias das tabelas que estão relacionadas, bem como podem ter seus próprios atributos. 

## Relacionamentos de grau maior que dois

Até o momento os relacionamentos trabalhados foram binários. A implementação de um relacionamento de grau maior que dois se dá nos seguintes passos:

1. O relacionamento se torna uma entidade, formando um relacionamento binário a cada uma das entidades que participavam do relacionamento original.
   
2. As regras de implementação citadas acima funcionam para relacionamentos binários deste mesmo tipo. 

A figura abaixo mostra um relacionamento ternário que é transformado em três relacionamentos binários:

![image](https://github.com/user-attachments/assets/9be2227c-83a8-4445-b21d-17dd70227994)

No primeiro exemplo temos um relacionamento ternário. Seguindo as regras recomendadas, transformamos este relacionamento em uma entidade, na qual terá uma relacionamento binário com cada uma das entidades que participavam do relacionamento. Sendo assim, o esquema para este modelo seria:

- **CIDADE(CodCidade, Nome)**
- **DISTRIBUIDOR(CodDist, Nome)**
- **PRODUTO(CodProd, Nome)**
- **DISTRIBUICAO(CodCidade,CodDist,CodProd, DataInicio)**
    - **CodCidade referencia CIDADE**
    - **Cod Dist referencia DISTRIBUIDOR**
    - **CodProd referencia PRODUTO**
 
## Implementação de generalização/especialização

Para implementar a tradução de uma generalização/especialização nós temos duas possibilidades: 

1- Uso de uma tabela para cada entidade
2- Uso de uma única tabela para toda hierarquia de generalização/especialização

A seguir discutiremos o uso de cada método, bem como quando utilizar cada alternativa.

### Uma tabela por hierarquia

Nesta alternativa, todas as tabelas referentes a entidade genérica e suas especializações serão transformadas em uma única tabela. Essa tabela deve ter:

- Chave primária correspondente ao identificador da entidade mais genérica.
- Caso não exista chave primária, uma coluna chamada *TIPO*, que será responsável por identificar cada entidade especializada.
- Uma coluna para cada atributo da entidade genérica.
- Uma coluna para cada atributo referente ao relacionamento que uma entidade genérica possui, e que os atributos dos relacionamentos foram passados para ela (entidade genérica).
- Uma coluna para cada atributo das entidades especializadas.
- Uma coluna para cada atributo referente ao relacionamento que uma entidade especializada possui, e que os atributos dos relacioanamentos foram pasados para ela (entidade especializada).

Considere uma tabela referente a uma entidade genérica chamada *Pessoa*, que possui as entidades especializadas *Aluno* e *Professor.* Uma possibilidade para representá-la é mostrada abaixo, onde uma única tabela é utilizada para representar tanto as entidades genéricas quanto a entidade especializada.

|ID|Nome|Curso|Disciplina|
|---|---|---|---|
|1|João|Computação|Banco de Dados I|
|2|Priscila|Engenharia|Estatística II|
|3|Igor|Medicina|Biomedicina II|

Neste caso, *ID* e *Nome* são atributos referentes a entidade genérica, enquanto *Curso* e *Disciplina* são atributos referentes a *Aluno* e *Professor*. Note que as regras propostas acima foram seguidas.

Agora vamos exemplificar a transformação de um modelo conceitual para um modelo lógico onde há o uso de generalização/especialização. Vamos também comentar algumas características referentes a junção da hierarquia em uma única tabela.

![image](https://github.com/user-attachments/assets/c8b04e73-77d5-4c57-a3c3-bf2fb967f8c8)

modelo lógico referente ao modelo conceitual acima é o seguinte:

- **DEPARTAMENTO(codDepto, nome)**
- **EMPREGADO (codEmp, nome, CIC, Tipo, codDepto, CartHab, CREA, codRamo)**
    - **codDepto Referencia DEPARTAMENTO**
    - **codRamo Referencia RAMO**
- **PROCTEXT(codProc, nome)**
- **DOMINIO(codEmp, codProc)**
    - **codEmp Referencia EMPREGADO**
    - **codProc Referencia PROCTEXT**
- **RAMO(codRamo, nome)**
- **PROJETO(codProj, nome)**
- **PARTICIPACAO(codEmp,codProj)**
    - **codEmp Referencia EMPREGADO**
    - **codProj Referencia PROJETO**

Note que nos relacionamentos 1:n foram criados chaves estrangeiras nas tabelas que tinham cardinalidade máxima n. Nos relacionamentos n:n construímos uma nova tabela referente ao relacionamento, contendo as chaves primárias das entidades que formam o relacionamento.

>Apenas os atributos das entidades especializadas são adicionadas na tabela generalizada. Portanto, é necessário verificar quem são os atributos das entidades especializadas, como chaves estrangeiras e atributos de relacionamentos.

A tabela EMPREGADO incluiu CREA, Habilitação e codRamo. Isto ocorre porque codRamo é passado como chave estrangeira para ENGENHEIRO, devido a natureza de seu relacionamento 1:n. Com isso, codRamo passa a ser um atributo em ENGENHEIRO, fazendo com que a entidade generalizada tenha um atributo referente a RAMO.

**OBS:** As colunas referentes as entidades especializadas devem, obrigatoriamente, serem definidas como opcionais, já que um registro da entidade genérica não contem os valores especializados simultaneamente.

### Uma tabela por entidade especializada

>É feita de maneira semelhante a tabela por hierarquia, com a única diferença sendo a adição da chave primária da entidade generalizada, nas entidades especializadas.

Para transformarmos uma generalização/especialização em um modelo lógico, podemos fazer a tradução através de uma tabela por entidade especializada. Neste caso teríamos, além da tabela genérica, todas as tabelas especializadas que contém algum atributo adicional além da chave primária. No caso da imagem acima, o modelo lógico seria o seguinte:

- **DEPARTAMENTO (*codDept*, nome)**
- **EMPREGADO (*codEmp*, Tipo, nome, CIC, codDept)**
    - **codDept Referencia DEPARTAMENTO**
- **MOTORISTA (*codEmp*, CartHab)**
    - **codEmp Referencia EMPREGADO**
- **ENGENHEIRO (*codEmp*, CREA, codRamo)**
    - **codEmp Referencia EMPREGADO**
    - **corRamo Referencia RAMO**
- **RAMO (*codRamo*, nome)**
- **PROJETO (*codProj*, nome)**
- **PARTICIPACAO (*codEmp*,*codProj*)**
    - **codEmp Referencia EMPREGADO**
    - **codProj Referencia PROJETO**
- **PROCTEXT (*codProc*, nome)**
- **DOMINIO (*codEmp*,*codProc*)**
    - **codEmp Referencia EMPREGADO**
    - **codProc Referencia DOMINIO**

Note que nas entidades especializadas, as chaves primárias também são chaves estrangeiras. Isso ocorre porque toda instância de uma entidade especializada será uma instância da entidade genérica.

### Vantagens de cada uma das alternativas

As vantagens em relação a uma tabela para toda hierarquia são:

- Pelo fato dos dados das entidades genéricas e especializadas estarem em uma única linha não há a necessidade de realizar junções numa consulta, caso desejar saber sobre informações das entidades especializadas e genéricas.
- Há um número menor de chaves primárias, fazendo com que haja uma eficiencia maior em termos de espaço, já que a chave primária cria um índice que ocupa um espaço consideravel.

As vantagens em relação a uma tabela para cada hierarquia especializada são:

- Quando vamos traduzir um modelo relacional em um modelo lógico temos duas possibilidades quando nos tratamos de generalização/especialização. Podemos ter o caso de uma única tabela representando a hierarquia, nesse caso, você terá atributos referentes a todas as tabelas especializadas, portanto terá valores nulos. Em contraste com uma tabela por hierarquia, onde cada atributo será referente aquela única tabela, diminuindo os atributos opcionais.

-**PRODUTO (*codProd*, CGC, NomeComercial, TipoEmbalagem, Quantidade, PrecoUnitario)**
    -**CGC Referencia FABRICANTE**
-**FABRICANTE (*CGC*, Nome, Endereco)**
-**MEDICAMENTO (*codProd*,CGC, Tarja, Formula)**
    -**CGC Referencia FABRICANTE**
-**PERFUMARIA (*codProd*, CGC,Tipo)**
    -**CGC Referencia FABRICANTE**
-**VENDA(*numNota*, Data, NomeCliente, CidadeCliente)**
-**PERFUMARIAVENDA(*codProd*, *numNota*, CGC, Quantidade, Imposto)**
    -**(codProd, CGC) Referencia PRODUTO**
    -**numNota Referencia VENDA**
    -**CGC Referencia FABRICANTE**
-**MEDICAMENTORECEITAVENDA (CRM, NumRec, numNota, Quantidade, Imposto)**
    -**numNota Referencia VENDA**
    -**(CRM, NumRec) Referencia RECEITAMEDICA**
-**RECEITAMEDICA(CRM,NumRec, Data)**



  




