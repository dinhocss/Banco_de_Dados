# Modelagem Conceitual
> A modelagem conceitual aplica conceitos de Entidade-Relacionamento para representação dos dados e suas relações.

Podemos definir um sistema de gerenciamento de banco de dados como um software responsável por fornecer funções que permitem realizar modificações, inserções, remoções sobre dados em um banco de dados. Para criarmos um banco de dados podemos utilizar o conceito de modelo de dados. Modelo de dados é uma representação das informações que determinado banco de dados vai armazenar. Por exemplo, ele irá definir quais serão as entidades do banco de dados, quais relacionamentos, quais os tipos de dados que os atributos terão, entre outros. Esse modelo de dados é representado na prática através da construção de um esquema. Um esquema em banco de dados é a representação das tabelas, atributos e relacionamentos que serão utilizados para guardar os registros.
Em um projeto de banco de dados geralmente são considerados dois níveis de abstração do modelo de dados, o **modelo conceitual** e o **modelo lógico**. 

O modelo conceitual nos fornece uma visão que independe de como os dados são implementados em um SGBD. Esse modelo registra quais dados aparecem em um banco de dados, mas não registra como esses dados são implementados.
A técnica mais utilizada para criar um modelo conceitual é a abordagem Entidade-Relacionamento (ER). Nesta técnica, um modelo conceitual é representado através de um diagrama, chamado diagrama Entidade-Relacionamento. Segue abaixo um exemplo de um modelo Entidade-Relacionamento:

![image](https://github.com/user-attachments/assets/ea5dfb6c-42f5-4bce-a0d9-9cf92a03db57)

A figura 1 representa um banco de dados através de um modelo conceitual, o modelo ER. Nesse modelo as entidades são representadas por retângulos e os relacionamentos por um losango. Cada entidade terá ligada a si seus atributos. 

**OBS:** O modelo lógico implementa um modelo conceitual. Portanto, primeiro partimos de um modelo que siga a abordagem ER, para em seguida utilizarmos o modelo lógico baseado nas informações do modelo conceitual.

***
# Abordagem Entidade-Relacionamento
>É uma técnica utilizada para implementar um modelo conceitual de um banco de dados.

Como visto anteriormente, em um projeto de criação de um banco de dados, a primeira etapa é dada pela utilização de um modelo conceitual. Esse modelo utiliza uma abordagem entidade-relacionamento para representar os dados contidos no banco de dados através de um diagrama, que contém as informações necessárias. A implementação desse modelo é dada através do modelo lógico, portanto o modelo conceitual é independente de como o código será implementado.

Nesta técnica o modelo de dados é representado através de um diagrama chamado *modelo Entidade-Relacionamento*. Esse diagrama conterá informações sobre as entidades e os relacionamentos entre essas entidades. Então o *modelo Entidade-Relacionamento* utiliza diversos termos que servem para representar como o esquema será feito, quais serão as entidades presentes, quais atributos referente a elas, entre outros.
***
# Entidade
Uma entidade representa um objeto do mundo real no qual se deseja obter e guardar informações. Em um diagrama Entidade-Relacionamento a entidade é representada através de um retângulo com seu nome no meio, como por exemplo:

![image](https://github.com/user-attachments/assets/80a3ff6c-d39d-462d-8ab1-daf6e5e1adb4)

Na figura 2 a entidade pessoa guardará uma coleção de objetos referentes aos atributos da pessoa, assim como departamento também guardará uma coleção de objetos. A representação de uma entidade em um banco de dados geralmente é feita como uma tabela. 

As entidades terão dentro de si um nome, atributos e instâncias da entidade. A representação desses atributos é dado por círculos ligados as entidades em questão. Cada linha da tabela referente a entidade será uma instância daquela entidade.
***
# Relacionamentos
Os relacionamentos representam um conjunto de associações entre entidades. Ou seja, como as entidades serão ligadas entre si. Em um diagrama Entidade-Relacionamento os relacionamentos são representados por um losango que é ligado nas entidades que participam desse relacionamento. Segue abaixo um exemplo de um relacionamento entre duas entidades:

![image](https://github.com/user-attachments/assets/7ce21007-b1a9-43aa-8df8-584695d87b7d)

Podemos usar também um diagrama de ocorrência. Esse diagrama também faz parte do modelo conceitual e nos fornece informações referentes as instâncias das entidades e como essas instâncias se relacionam entre si. 

🎯[Como funciona um diagrama de ocorrência?](https://github.com/dinhocss/Banco_de_Dados/wiki/Anota%C3%A7%C3%B5es-complementares#como-funciona-um-diagrama-de-ocorr%C3%AAncia)

Um relacionamento nem sempre associa entidades diferentes. Pode haver casos em que um relacionamento está ligado a somente uma entidade. Nesse caso, a entidade contém um auto relacionamento. Segue abaixo um diagrama ER que possui uma entidade que tem um auto relacionamento:

![image](https://github.com/user-attachments/assets/9f287f26-61fb-4465-b372-eb1928c36c14)

No caso de auto relacionamento é necessário um conceito adicional, que é o conceito de papel que uma entidade  terá num relacionamento. No exemplo acima temos um marido representando um papel de uma instância da entidade pessoa e uma esposa representando um papel de uma outra instância da entidade pessoa. Podemos representar os auto relacionamentos em diagramas de ocorrência como o exemplo abaixo:

![image](https://github.com/user-attachments/assets/70179163-78d0-42a4-9fc2-c970289a8817)

***
# Cardinalidade

A cardinalidade em um banco de dados define a quantidade de instâncias de uma entidade que podem estar associadas a uma instância de outra entidade. A cardinalidade é utilizada para descrever como as entidades se relacionam em termos de ocorrência. Essas cardinalidades podem ser máximas ou mínimas.

A *cardinalidade máxima* refere-se a quantidade máxima de instâncias  de uma entidade que podem estar associadas a uma única instância de outra entidade. Já a *cardinalidade mínima* refere-se a quantidade mínima de ocorrências de uma entidade que pode estar relacionada a uma única instância de outra entidade. 

A cardinalidade é representada num diagrama ER de maneira pouco convencional, pois a quantidade de ocorrências máximas ou mínimas de uma entidade é descrita na parte contrária da entidade analisada. Segue abaixo um exemplo de como essa representação é feita:

![image](https://github.com/user-attachments/assets/831d6afe-d74c-4bff-ab8d-c95a3bf8f8c8)

O significado dos relacionamentos acima é que cada empregado pode estar associado com no máximo um departamento, e cada departamento pode estar associado a diversos empregados.

***

# Tipos de Relacionamentos

Os relacionamentos podem variar dependendo da cardinalidade entre as entidades. Podemos ter relacionamentos do tipo 1:1 (um pra um), 1:n, (um pra muitos), n:n (muitos pra muitos). Segue abaixo alguns exemplos de cada tipo de relacionamento:

## Relacionamento 1:1

São relacionamentos no qual as entidades podem ter no máximo 1 instância relacionada entre elas, como pode ser visto no exemplo abaixo:

![image](https://github.com/user-attachments/assets/2e7aabc6-1f18-4927-a8cf-e5b3841da510)

Representamos com o número 1 para indicar que uma entidade possui cardinalidade 1. E o diagrama acima diz que cada empregado terá somente uma mesa, e cada mesa deverá ser ocupada por apenas um empregado.

## Relacionamento 1:n

No caso de relacionamentos 1:n temos que uma instância de uma determinada entidade estará relacionada a várias instâncias de outra entidade. Considere a figura abaixo que demonstra alguns relacionamentos 1:n:

![image](https://github.com/user-attachments/assets/e04826a2-bc20-4bae-b822-798abe8e21be)

A figura 8 mostra alguns relacionamentos 1:n. A leitura correta dos diagramas é que um aluno está matriculado em um curso, mas um curso pode ter vários alunos; um empregado pode ter vários dependentes, mas um dependente está vinculado a apenas um empregado, e um empregado é supervisionado por um único supervisor, enquanto um supervisor supervisiona vários empregados.

## Relacionamento n:n

Em relacionamentos n:n temos que uma instância de uma entidade está envolvida com várias instancias de outra entidade, e vice-versa. Por exemplo, considere a figura 9 que mostra alguns relacionamentos n:n:

![image](https://github.com/user-attachments/assets/a81b3c4e-61f9-49a1-bcc4-1d0509e0130f)

A tradução dos relacionamentos acima é: um engenheiro pode estar associado a vários projetos, e um projeto pode ter diversos engenheiros; um médico pode ter vários pacientes, e um paciente pode se consultar com vários médicos; uma peça pode ter vários fornecedores, e um fornecedor pode ter várias peças, e por último, um produto possui diversos componentes, e um componente pode estar presente em diversos produtos.

## Relacionamentos Ternários

Os exemplos vistos anteriormente são de relacionamentos binários, porém, o modelo ER possibilita a existência de relacionamentos ternários, que relacionam três entidades ou mais a um mesmo relacionamento. Segue abaixo um exemplo de um relacionamento ternário:

![image](https://github.com/user-attachments/assets/161c1905-e7ce-46f4-8222-a6fa44dbf189)

No caso de relacionamentos ternários também temos o conceito de cardinalidade máxima e cardinalidade mínima. Por exemplo, a figura abaixo mostra as cardinalidades referentes ao relacionamento ternário acima:

![image](https://github.com/user-attachments/assets/2fe37f4a-1396-47a6-853e-f9a2d917277e)

As cardinalidades acima dizem que um distribuidor pode ter um produto em diversas cidades, também que um produto distribuído em uma cidade só pode ter um único distribuidor, e por último que um distribuidor em uma cidade pode ter diversos produtos.

***
## Cardinalidade Mínima

Além da cardinalidade máxima uma outra característica que podemos ter num diagrama ER é a cardinalidade mínima, que indica o número mínimo de ocorrências que uma determinada entidade terá em relação a uma ocorrência de outra entidade. Considera-se a cardinalidade mínima como sendo 1 ou 0.

A cardinalidade 1 é denominada *associação obrigatória*, já que o mínimo de ocorrências que uma instância terá em relação a ocorrência de uma outra instância será 1. E a cardinalidade 0 é denominada *associação opcional*.

A figura 12 mostra um relacionamento com cardinalidades máxima e mínima, e um diagrama de ocorrência desse relacionamento 1:1:

![image](https://github.com/user-attachments/assets/7ea1c5f1-adf5-4a58-b6fc-a2755afd05f7)

A figura acima traduz-se em um empregado está associado a uma única mesa, e uma mesa pode ter 0 ou 1 empregados alocados nela.

💻[Exemplo completo de um diagrama Entidade-Relacionamento](https://github.com/dinhocss/Banco_de_Dados/wiki/Anota%C3%A7%C3%B5es-complementares#exemplo-completo-de-um-diagrama-entidade-relacionamento)
***

## Atributos

Um atributo é um dado que é associado a cada ocorrência de uma entidade ou relacionamento. Os atributos são demonstrados graficamente através de um círculo branco ligado a determinada entidade ou relacionamento, por exemplo:

![image](https://github.com/user-attachments/assets/4b0d97e3-d268-4d99-9416-d417f3857a6d)

No caso acima temos tambem uma notação parecida com a notação de relacionamentos, onde há cardinalidade mínima e máxima. 

Uma outra característica de atributos é que eles podem estar relacionados a relacionamentos também. Por exemplo:

![image](https://github.com/user-attachments/assets/fe17a65e-da5f-4e34-ba97-1abb0390c6b6)

Nesse caso temos um atributo relacionado ao relacionamento Atuação. Este atributo não pode estar em engenheiro, pois um mesmo engenheiro pode ter funções diferentes em diferentes projetos. E também não pode estar em projeto, pois um projeto pode ter mais de um engenheiro com funções diferentes.



***

## Identificando Entidades

