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
# Cardinalidade Mínima

Além da cardinalidade máxima uma outra característica que podemos ter num diagrama ER é a cardinalidade mínima, que indica o número mínimo de ocorrências que uma determinada entidade terá em relação a uma ocorrência de outra entidade. Considera-se a cardinalidade mínima como sendo 1 ou 0.

A cardinalidade 1 é denominada *associação obrigatória*, já que o mínimo de ocorrências que uma instância terá em relação a ocorrência de uma outra instância será 1. E a cardinalidade 0 é denominada *associação opcional*.

A figura 12 mostra um relacionamento com cardinalidades máxima e mínima, e um diagrama de ocorrência desse relacionamento 1:1:

![image](https://github.com/user-attachments/assets/7ea1c5f1-adf5-4a58-b6fc-a2755afd05f7)

A figura acima traduz-se em um empregado está associado a uma única mesa, e uma mesa pode ter 0 ou 1 empregados alocados nela.

💻[Exemplo completo de um diagrama Entidade-Relacionamento](https://github.com/dinhocss/Banco_de_Dados/wiki/Anota%C3%A7%C3%B5es-complementares#exemplo-completo-de-um-diagrama-entidade-relacionamento)
***

# Atributos

Um atributo é um dado que é associado a cada ocorrência de uma entidade ou relacionamento. Os atributos são demonstrados graficamente através de um círculo branco ligado a determinada entidade ou relacionamento, por exemplo:

![image](https://github.com/user-attachments/assets/4b0d97e3-d268-4d99-9416-d417f3857a6d)

No caso acima temos tambem uma notação parecida com a notação de relacionamentos, onde há cardinalidade mínima e máxima. 

Uma outra característica de atributos é que eles podem estar relacionados a relacionamentos também. Por exemplo:

![image](https://github.com/user-attachments/assets/fe17a65e-da5f-4e34-ba97-1abb0390c6b6)

Nesse caso temos um atributo relacionado ao relacionamento Atuação. Este atributo não pode estar em engenheiro, pois um mesmo engenheiro pode ter funções diferentes em diferentes projetos. E também não pode estar em projeto, pois um projeto pode ter mais de um engenheiro com funções diferentes.

***

# Identificando Entidades

Cada entidade deve possuir um identificador. Um identificador é um conjunto de um ou mais atributos cujos valores servem para distinguir uma ocorrência da entidade das demais ocorrências dessa mesma entidade. Em outras palavras, ele é utilizado para identificar de maneira única cada registro dentro de uma tabela em um banco de dados. No diagrama Entidade-Relacionamento, os identificadores são representados por círculos pretos ligados as entidades ou relacionamentos. 

O caso mais simples ocorre quando a entidade possui um único identificador. Podendo ser representada da seguinte maneira:

![image](https://github.com/user-attachments/assets/229f4ef2-d93f-47d6-8370-42f364c332b9)

Podemos ter o caso de uma entidade possuir mais de um atributo como identificador, como por exemplo:

![image](https://github.com/user-attachments/assets/bfe5aded-4fba-4e11-b888-2da7e20591de)

No caso acima temos um identificador composto por dois atributos. Isso significa que para cada instância de prateleira nós teremos um número de corredor e um número de prateleira associada a ela. 

Em último caso podemos ter também uma entidade que possui não só um atributo seu como identificador, como também possui atributos de outras entidades que estão ligadas por algum relacionamento. Por exemplo:

![image](https://github.com/user-attachments/assets/75544b65-5a4a-41be-9069-3e46f85cea42)

>Entidade fraca é uma entidade que possui um identificador primário em sua tabela proveniente de outra entidade.

O termo fraca significa que cada ocorrência da entidade de dependente existirá somente se existir uma ocorrência da entidade empregado. Uma entidade fraca é representada por um risco mais grosso ligando a entidade ao relacionamento.

O modelo ER acima diz o seguinte: *um empregado pode ter nenhum ou vários dependentes*, e *um dependente está relacionado com, obrigatoriamente, um empregado.* Os atributos de EMPREGADO são o *código* (identificador primário) e o *nome*. Já os atributos de DEPENDENTE são o *número da sequencia* e o *código do empregado* como identificadores primários (composto), e o *nome*.

***

# Identificando Relacionamentos

Em casos de relacionamentos do tipo n:n (muitos pra muitos), geralmente criamos uma tabela extra chamada tabela associativa ou tabela de junção. Essa tabela irá conter como identificador primário uma combinação das chaves primárias provenientes de cada entidade que está ligada ao relacionamento. A ocorrência de um relacionamento advém da ocorrência de cada instância da entidade participante do relacionamento.

Podemos também ter o caso em que uma ocorrência de duas entidades que estão em um relacionamento está associado a ocorrência de varias instâncias de relacionamento. Por exemplo, considere a imagem abaixo:

![image](https://github.com/user-attachments/assets/4b17d2d6-196c-4a19-b5b8-47ec99256426)

De acordo com a figura acima, um médico pode ter consulta com diversos pacientes, e um paciente pode se consultar com diversos médicos. O identificador em data/hora faz com que toda consulta seja registrada, pois um mesmo paciente pode ter diversas consultas com um mesmo médico.

**OBS:** Caso não fosse definido como atributo primário o atributo data/hora, cada nova consulta com o mesmo médico apagaria o registro da consulta anterior.

***

# Generalização/Especialização

O conceito de generalização/especialização em um modelo ER diz respeito a uma hierarquia de entidades,  onde uma entidade genérica fornece atributos  comuns a todas as entidades especializadas, enquanto as entidades mais especializadas pode conter atributos mais específicos. O símbolo que representa uma generalização/especialização é um triângulo isósceles, como mostrado abaixo:

![image](https://github.com/user-attachments/assets/5e96fd51-2da1-49ab-b8a5-ab1c573f485c)

A tradução do modelo acima é que *uma filial está relacionada a nenhum ou vários clientes*, e *um cliente está relacionado, obrigatoriamente, a uma filial*. E cliente pode ser pessoa física ou pessoa jurídica. As entidades especializadas possuem atributos próprios, assim como os atributos herdados da entidade genérica. 

A generalização/especialização pode ser dividida em dois tipos: A total e parcial. Ela será definida entre uma das duas de acordo com a obrigatoriedade ou não de uma ocorrência da entidade genérica corresponder a uma ocorrência da entidade especializada.

## Generalização/especialização total

Ocorre quando a ocorrência de uma entidade genérica tem que, obrigatoriamente, estar relacionada a uma ocorrência de uma entidade especializada, como por exemplo:

![image](https://github.com/user-attachments/assets/3ad5f6a6-8c01-42c4-8fed-93e2ecd6d3f2)

Na figura acima, cada instância de cliente precisa estar associada, obrigatoriamente, a entidade pessoa física ou pessoa jurídica. O símbolo que representa uma generalização/especialização total é o t. 

## Generalização/especialização parcial

Neste caso nem toda ocorrência da entidade genérica precisa estar associada a uma ocorrência da entidade especializada. Segue abaixo um exemplo de uma generalização/especialização parcial:

![image](https://github.com/user-attachments/assets/d02b416a-e401-4679-b2ae-c1ed5e42b86e)

A figura acima mostra a situação na qual um funcionário pode não ser nem motorista, nem secretária. Sendo assim, não há uma obrigatoriedade de associar uma instância de funcionário a uma instância mais generalizada. Quando temos generalização/especialização parcial, geralmente temos também um atributo que define o tipo de ocorrência da entidade genérica. O símbolo que representa uma generalização/especialização parcial é o p.

## Níveis de hierarquia na generalização/especialização

Uma entidade pode ser especializada em qualquer número de entidades, inclusive em uma. No exemplo da generalização/especialização parcial, se a entidade motorista for a única que possui atributos particulares, então ele será a única entidade especializada. Além disso, não há limites no número de níveis hierárquicos da generalização/especialização. Uma entidade generalizada pode ser genérica para outras entidades. É possível inclusive que uma mesma entidade seja especialização de diversas classes genéricas, que é chamada de herança múltipla. Segue abaixo um exemplo de diferentes níveis de hierarquia e herança múltipla:

![image](https://github.com/user-attachments/assets/c0a41236-391c-4e12-a1e2-c83f279b34c1)

A figura acima diz que um barco é especialização de uma entidade genérica, que por sua vez, também é uma entidade especializada de outra entidade genérica. A entidade barco possui atributos próprios, bem como atributos herdados das entidades veículo aquático e veículo. 

O exemplo de herança múltipla se dá através da entidade *veículo anfíbio*, em que uma mesma entidade especializada herda atributos tanto da entidade genérica *veículo terreste* quanto da entidade *veículo aquático.*

**OBS:** A fonte de estudos trata a generalização/especialização como exclusiva, ou seja, uma instância de veículo deve corresponder a um automóvel, um veículo anfíbio ou um barco. Não podemos ter uma mesma instância associada a mais de uma entidade especializada.

***
# Entidade Associativa

Um relacionamento na modelagem de dados é dado por uma associação entre entidades, como exemplificado abaixo:

![image](https://github.com/user-attachments/assets/a7048cf8-8e53-4338-b45f-4b5d079d1f0d)

De acordo com a figura acima, temos uma entidade MÉDICO que possui uma relação muitos pra muitos com a entidade PACIENTE. Se quisermos registrar os medicamentos que foram prescritos nesta consulta, precisamos relacionar esses medicamentos  a própria consulta, e isso não é possível de fazer quando a consulta é um relacionamento. Nesses casos, criamos uma entidade associativa, fazendo com que CONSULTA agora seja uma entidade própria. Assim, CONSULTA pode ter atributos adicionais, como data, hora, entre outros. 

A representação gráfica de uma entidade associativa é um retângulo em torno do relacionamento que liga as entidades desejadas, como por exemplo:

![image](https://github.com/user-attachments/assets/8bf3f75d-a4d6-4731-a1c2-d827030ed79b)

Note que agora é possível associar relacionamentos entre si, pois a entidade associativa atua simultaneamente como entidade e como relacionamento. Isso permite que haja diferentes registros referentes a uma mesma associação MÉDICO e PACIENTE. Caso não houvesse essa tabela associativa, somente o último registro seria guardado, pois não haveria modo de diferenciar a ocorrência da associação MEDICO e PACIENTE.  

## Uma alternativa a entidade associativa

Uma alternativa ao exemplo dado no tópico de entidade associativa é apresentada abaixo:

![image](https://github.com/user-attachments/assets/c2220d87-9ec4-4b2a-9cd2-ca81271df2b1)

A alternativa é tornar a consulta uma tabela que possua um relacionamento n:1 tanto com paciente, quanto com médico. Note que o relacionamento entre CONSULTA e MÉDICO é 1:1, bem como o relacionamento entre CONSULTA e PACIENTE.

***

# Propriedades de modelos ER

Algumas propriedades podem ser atribuídas a modelos ER, como por exemplo:

1. **Um modelo ER é um modelo formal**
    - Isso significa que um banco de dados deve ser entendido por diferentes pessoas, e que é necessário ter um conhecimento sobre modelagem ER para conseguir realizar uma leitura correta de um modelo ER.
2. **A abordagem ER tem poder de expressão limitado**
    - Isso significa que não podemos representar todos os atributos e características de um banco de dados através de um modelo ER. Muitas vezes há algumas características que não podem ser representadas em um modelo. É necessário que a pessoa que irá modelar o banco de dados saiba equilibrar a necessidade de modificar modelos ER para melhor entendimento ou quando abstrair informações que não serão relevantes durante a modelagem.
3. **Diferentes modelos podem ser equivalentes**
    - Dois modelos ER são equivalentes quando, ao serem implementados através do modelo lógico, gerem o mesmo Banco de Dados. Isto significa que ambos os modelos ER devem possuir a mesma implementação lógica, com as mesmas características (podendo ser abstraídos os nomes de atributos e de entidades), resultando em um único Banco de Dados. Por exemplo, no caso abaixo temos duas modelagem diferentes, sendo elas:
      ![image](https://github.com/user-attachments/assets/3a161c43-fcf3-42c9-be03-9649cc4fa1ae)
   - Os dois exemplos acima configuram o mesmo Banco de Dados, modelado de maneiras diferentes, porém com as mesmas características. Na primeira figura temos um relacionamento n:n que associa as entidades MEDICO e PACIENTE. Já no segundo exemplo, esse relacionamento n:n foi transformado em uma entidade. Essa equivalência é bastante comum, tendo um passo a passo para realizar essa equivalência, sendo eles:
     - O relacionamento n:n é representado como uma entidade.
     - A entidade criada é relacionada com as entidades que originalmente participavam do relacionamento.
     - A entidade criada tem como identificador:
        - As entidades que participavam do relacionamento original.
        - Os atributos identificadores das entidades originais (caso tenha).
     - As cardinalidades dos relacionamentos da entidade criada é sempre 1:1.

***

# Identificando Construções

Quando queremos modelar um objeto do mundo real para uma abordagem ER temos diversas possibilidades diferentes. Muitas vezes a decisão a ser tomada em relação a um objeto ser modelado como atributo, entidade ou relacionamento dependem do contexto dado. Conforme vamos criando e modelando um banco de dados, podemos e devemos realizar modificações conforme a necessidade vai surgindo. Portanto, não é recomendado ficar muito tempo preso num mesmo conceito.

## Como decidir entre modelar um objeto como sendo um atributo, ou um relacionamento?

A figura abaixo apresenta duas possibilidades de modelagem de um mesmo objeto (cor):

![image](https://github.com/user-attachments/assets/17a1c3f5-3be6-4cb9-9ffe-3614cadb79cc)

A decisão de modelar um objeto como atributo ou como entidade depende de alguns fatores, sendo eles:

1. **Vinculação a outros objetos**
    - Quando o objeto em questão tiver relacionado a outros objetos ou tiver atributos próprios, ele deverá ser modelado como uma entidade. Isso ocorre porque atributos não podem ter seus próprios atributos ou se relacionar diretamente a outras entidades.
    - No exemplo acima, se a cor do automóvel possuir características, como por exemplo, fabricante da cor ou subtom, o objeto deve ser modelado como uma entidade. Caso a cor seja apenas uma informação isolada, ela pode ser modelada como atributo do automóvel.
2. **Domínio de valores fixo ou mutável**
    - Se o conjunto de valores for fixo durante toda vida do sistema, ele pode ser modelado como um atributo. Por exemplo, se tivermos uma quantidade fixa de cores disponíveis, podemos modelar esse conjunto de cores como atributo de automóvel. Caso o conjunto de valores a ser modelado se modifica com o tempo, então é necessário modelar o objeto como uma entidade.
    - Por exemplo, se temos as opções, verde, vermelho e preto para um determinado carro, o objeto cor pode ser modelado como um atributo. Caso haja a necessidade de adicionar mais cores futuramente então o objeto deverá ser modelado como entidade.
### Resumindo
- Se o objeto tiver relacionamento com um outro objeto, ou se o objeto tiver atributos próprios, então ele deverá ser uma entidade; Se o objeto possuir um conjunto de valores variável, então ele deverá ser uma entidade; Se o objeto possui um conjunto de valores fixos, e não possua vínculos com outros objetos, então dele deverá ser um atributo.

## Como decidir entre modelar um objeto como sendo um atributo ou uma generalização/especialização?

Considere os dois casos abaixo:

![image](https://github.com/user-attachments/assets/65c6b24e-b300-4128-ba02-7285a1837561)

No exemplo dado podemos escolher entre ter um atributo relacionado a categoria funcional de determinado empregado, ou podemos utilizar a generalização/especialização para definir que empregado é uma entidade genérica, em que as entidades especializadas também são definidas. A decisão de escolher entre modelar um objeto como atributo ou como uma generalização/especialização depende se as entidades especializadas possuem alguma característica própria. No caso acima somente um engenheiro possui CREA, assim como o motorista precisa de habilitação. 

**OBS:** Não é recomendado utilizar atributos opcionais ou multi-valorados em entidades. Geralmente, atributos opcionais podem fazer parte de entidades especializadas, tornando necessário uma abordagem de generalização/especialização. No caso de atributos multi-valorados, a linguagem SQL não possui implementação direta a esse recurso.

***

# Como fazer a verificação do modelo para saber se está correto?

Ao criarmos nosso modelo ER, precisamos verificar se o mesmo se encontra dentro das “regras” da modelagem. Para um modelo ser considerado bom ele deve seguir uma série de requisitos, como ser completo, ser correto e não conter redundâncias. Segue abaixo uma breve explicação de cada requisito:

## Modelo Correto

Para um modelo ER ser considerado correto precisamos garantir que não haja erros de modelagem. Os erros de modelagem podem ser divididos em dois tipos, os *erros sintáticos* e os *erros semânticos*.

- **Erros sintáticos:** ocorrem quando o modelo não respeita as regras de construção de um modelo ER. Por exemplo, associar atributos a outros atributos, associar relacionamentos a outros relacionamentos, especializar relacionamentos ou atributos, entre outros.
- **Erros semânticos:** ocorrem quando o modelo não representa a realidade de forma consistente. Alguns exemplos de erros semânticos são: estabelecer associações incorretas, usar uma entidade do modelo como atributo de outra entidade, usar o número incorreto de entidades em um relacionamento, entre outros.

## Modelo Completo

Para um modelo ser considerado completo ele precisa ter todas as propriedades desejáveis do banco de dados. Isso significa que:

- **Todos os dados relevantes estão presentes no modelo:** O modelo deve conter todas as entidades e relacionamentos necessários para armazenar as informações que o sistema precisa.
- **As transações de modificação podem ser executadas:** Todas as operações sobre os dados, como inserções, atualizações e exclusões, devem ser devidamente implementadas conforme a necessidade do sistema. Assim, o banco de dados suportará as operações necessárias para a manutenção do sistema.

## Modelo livre de redundâncias

Um modelo deve ser mínimo, isto é, livre de conceitos redundantes. No conceito de banco de dados, a palavra redundante é abstrata e depende da interpretação do modelador. Por exemplo, considere o exemplo abaixo:

![image](https://github.com/user-attachments/assets/e959d678-ae11-442c-9c89-8d328806a586)

No diagrama exibido as linhas em negrito representam relacionamentos redundantes. O relacionamento ATUAÇÃO entre SINDICATO e FÁBRICA pode ser obtido através do relacionamento entre FÁBRICA e EMPREGADO. Caso um sindicato esteja associado a um empregado, ele estará alocado em um departamento, que está dentro de uma fábrica. O mesmo pode ser dito do relacionamento entre MÁQUINA e FÁBRICA. Esse relacionamento pode ser obtido através do relacionamento LOCALIZAÇÃO DEPTO.

Apesar de termos dois caminhos entre FÁBRICA e MÁQUINA, ambos os caminhos são necessários. Para verificarmos a redundância não basta apenas verificarmos se os caminhos são comuns. É preciso também analisar o contexto e o significado do relacionamento. No exemplo acima o relacionamento entre DEPTO e MÁQUINA representa o departamento em que as máquinas estão alocadas. Já o relacionamento entre EMPREGADO e MÁQUINA  representa a máquina que cada empregado está operando. São conceito diferentes e precisam ser expressados separadamente.

Podemos verificar se um relacionamento é redundante ao tentarmos tirar o relacionamento da modelagem. Caso o modelo perca o sentido ou falte informações importantes, então o relacionamento não será redundante.

Um outro tipo de redundância que pode aparecer em modelos ER são atributos redundantes. Quando temos um atributo que pode ser obtido automaticamente através de cálculo ou de busca no banco de dados, não tem sentido armazená-lo. Armazenar um atributo desse tipo configura em uma redundância. Por exemplo, se temos uma entidade que possuí a data de nascimento como atributo, seria redundante adicionar um atributo referente a idade, pois a idade pode ser calculada através da data de nascimento.

## Modelo deve refletir o aspecto temporal

O modelo do banco de dados deve refletir não apenas o estado atual do dado, mas também ter a flexibilidade de lidar com informações que mudam ao longo do tempo. Algumas informações podem variar com o tempo, e é essencial identificar essas informações para planejar como o banco de dados irá trabalhar com elas.

***

# Estratégias de Modelagem

Podemos ter diferentes técnicas para modelar um banco de dados. Primeiramente devemos verificar qual será a fonte de informação que nosso modelo irá se basear. As fontes de informação podem ser dados existentes ou o conhecimento do modelador em relação ao sistema. As estratégias de modelagem nos fornecem um passo a passo de como modelar um banco de dados.

## Partindo de dados existentes

Uma possibilidade de fonte de informação para o processo de modelagem de dados são descrições de dados já existentes. Dentro desse contexto podemos ter duas situações. Uma delas é quando temos um sistema de banco de dados já existente e implementado e queremos criar um modelo conceitual para esse sistema. Nesse caso, utilizamos a estratégia engenharia reversa, no qual a partir de um sistema já pronto, nós construímos um modelo para esse sistema.

Podemos também modelar um banco de dados a partir de documentos físicos ou não automatizados. Nesse caso, uma boa estratégia é a “bottom-up”, no qual começamos a partir dos atributos, em seguida identificando as entidades, e por fim, o relacionamento. Essa forma é adequada de se trabalhar quando já se dispõe dos atributos.

## Partindo do conhecimento de pessoas

Este é o caso de sistemas que estão sendo criados do zero, onde não há informações sobre os dados existentes. Neste caso caso podemos utilizar duas estratégias, sendo elas, “top-down” e “inside-out”.

1. **Top-down**
    - Nesta estratégia parte-se dos conceitos mais abstratos, detalhando estes conceitos conforme novos dados forem sendo inseridos. Aqui o processo de modelagem inicia-se através da identificação de entidades genéricas. A partir dai define-se os atributos dessas entidades, seus relacionamentos, os atributos de seus relacionamentos, e a especialização de entidades.
    - Uma sequencia de passos realizados para construir um modelo através da estratégia “top-down” é mostrado abaixo:
        1. *Modelagem superficial* - Nesta primeira etapa, é construído um DER pouco detalhado na seguinte sequência:
            1. Enumeração das entidades.
            2. Identificação dos relacionamentos e hierarquias de generalização/especialização entre entidades. Para cada relacionamento identifica-se a cardinalidade máxima.
            3. Determinação dos atributos de entidades e relacionamentos.
            4. Determinação dos identificadores de entidades e relacionamentos.
            5. O banco de dados é verificado quanto ao aspecto temporal.
        2. *Modelagem detalhada* - Nesta etapa, completa-se o modelo com o domínio dos atributos e a cardinalidade mínima do relacionamento:
            1. Adiciona-se o domínio dos atributos.
            2. Determina-se a cardinalidade mínima dos relacionamentos.
            3. Define-se as demais restrições de integridade que não podem ser representadas pelo DER
        3. *Validação do modelo* 
            1. Procura-se construções redundantes.
            2. Valida-se o modelo com o usuário.
2. **Inside-out**
    - Parte de conceitos mais importantes e ir gradativamente adicionando conceitos a eles relacionados. Neste caso, iniciamos com a identificação de uma entidade de maior importância no modelo. A partir dai, procura-se entidades relacionadas, bem como atributos e relacionamentos referentes a essa entidade.
  
***









