> **Normalização**: É um processo no design do banco de dados que organiza os dados de modo a diminuir a quantidade de redundâncias e dependências indesejadas.

# Composição de um banco de dados relacional

Um banco de dados relacional é composto por tabelas ou relações, dentro dessas tabelas temos atributos, chaves primárias, chaves estrangeiras, entre outros.

## Tabelas

Uma tabela é um *conjunto não ordenado* de linhas (ou tuplas). Cada linha é composta por uma série de campos (atributos). Cada campo é identificado pelo nome do campo (nome do atributo). O conjunto de campos de mesmo nome formam uma coluna. 

![image](https://github.com/user-attachments/assets/a269fa37-a0cc-4ae2-88ca-5b27bd26acc5)

Segue algumas características referentes as tabelas:
* Cada linha é uma lista de valores, ou seja, a ordem que representamos os elementos dessa lista importa.
* Cada atributo possui um nome e um domínio.
  * Exemplo: **nome: varchar(30), matricula: integer, dataNasc: date**
* O grau de uma tabela representa o número de atributos que ela tem
* A cardinalidade da tabela representa o número de linhas que ela possui.
Segue abaixo uma representação desses conceitos:

![image](https://github.com/user-attachments/assets/c031e780-3a39-490e-8e16-4181f39b0e4a)

## Chaves

O conceito básico que permite estabelecer relações entre duas tabelas é o de chaves. Em um modelo relacional, temos três tipos de chaves: Chave Primária, Chave Alternativa e Chave Estrangeira.

### Chave primária

Uma chave primária é uma coluna ou uma combinação de colunas cujo valor não se repete. Na figura 1.1 temos a tabela Emp, no qual sua chave primária é dada pelo atributo CódigoEmp. Agora, caso a gente queira registrar os dependentes de cada empregado, apenas um identificador não será suficiente. Considere a tabela de dependente abaixo:

![image](https://github.com/user-attachments/assets/4b42544d-63d3-403d-8206-9c24ea4c1c56)

A chave primária é uma chave composta dada por CódigoEmp e NoDepen. É necessária uma chave composta pois um mesmo empregado por ter dois dependentes, portanto não seria possível ter dois registros com o mesmo valor de chave primária.  

**OBS:** É necessário que a chave primária seja mínima. Ou seja, quando somente as colunas necessárias para identificação da entidade são utilizadas.

### Chave estrangeira

Uma chave estrangeira é uma coluna ou uma série de colunas, cujos valores aparecem, obrigatoriamente, na chave primária de uma tabela. A chave estrangeira permite o relacionamento entre tabelas. Na figura 4.3 o atributo CodigoDepto da tabela Emp é uma chave estrangeira em relação a CodigoDepto da entidade Dept. Isso significa que cada instância de Emp deve estar associada com um CodigoDepto existente na tabela Dept. 

![image](https://github.com/user-attachments/assets/cdd756fe-a7d7-44b6-8b98-ab4fd7ba6224)

Para garantir a integridade referencial dos dados, nós devemos seguir algumas regras em relação a manipulação de chaves estrangeiras. Sendo essas regras:

- Quando adicionamos um novo registro em uma tabela que tenha chave estrangeira, o valor dessa chave deve existir na tabela que contém a chave referenciada.
- Ao modificarmos o valor de uma chave estrangeira, precisamos garantir que o novo valor escolhido esteja na tabela que contém a chave referenciada.
- Ao excluirmos um registro da tabela referenciada, precisamos garantir que não há nenhuma chave estrangeira que está referenciando o registro na tabela referenciada.

Uma chave estrangeira pode existir também dentro da própria tabela na qual ela faz referência. Por exemplo, considere a imagem abaixo:

![image](https://github.com/user-attachments/assets/3979601d-304b-435d-b693-28805f52da1f)

Na figura 4.4 temos uma chave estrangeira que faz referência a uma chave primária da própria tabela. Por exemplo, considere a imagem abaixo:

Ao removermos ou atualizarmos uma chave primária no banco de dados, há um padrão default para lidar com qualquer tabela que esteja referenciando esses valores atualizados ou deletados. Por exemplo:

![image](https://github.com/user-attachments/assets/ac29c73e-d5ed-457c-a79d-c82c8e061b9f)

Podemos lidar com a remoção da chave primária D2 de quatro maneiras diferentes:

- **Opção 1 (default):** Bloqueia a tentativa de remoção de uma linha referenciada em outra tabela (on delete restrict)
- **Opção 2:** Propaga a remoção, ou seja, tudo que tiver referenciando a chave primária D2 será removido (on delete cascade)
- **Opção 3:** Propaga o valor nulo (on delete set null)
- **Opção 4:** Propaga o valor default do atributo que forma a chave estrangeira (on delete set default)

**OBS:** O procedimento de atualização segue o mesmo princípio e possui as mesmas opções.

### Chave alternativa

Uma chave alternativa é um atributo ou um conjunto de atributos que poderia ser usado como chave primária na tabela, pois é único e identifica cada registro da tabela de forma exclusiva. No entanto, ao invés de ser escolhida como chave primária, é escolhida como chave alternativa. 

Quando temos mais de um candidato para representar a chave primária, geralmente escolhemos um e os outros serão chaves alternativas. As chaves alternativas possuem as mesmas características de chaves primárias em termos de unicidade. 

As chaves alternativas são uteis quando precisamos fazer consultas usando outros identificadores únicos, além do primário. Quando tornamos uma chave em alternativa, o SGBD automaticamente cria um índice pra ela, tornando as operações sobre a chave mais rápidas e eficientes. Por esse motivo, a busca em chaves alternativas é mais eficiente do que em atributos normais. 

Quando levamos em consideração as chaves primárias e chaves alternativas dentro de uma tabela, elas se assemelham bastante, pois ambas possuem um registro único na tabela, e ambas não podem ser nulas. Porém, a maior diferença se dá quando precisamos referenciar a tabela através de uma chave estrangeira em outra tabela. Nesse caso, a chave estrangeira estará relacionada à chave primária, portanto é necessário levar em consideração essa questão ao definir quem será a chave primária.


## Domínio e valores vazios

>Domínio é o conjunto de valores que um determinado atributo pode assumir.

Quando uma tabela de um banco de dados é definida, para cada coluna da tabela, deve-se especificar um conjunto de valores (numéricos, alfanumérico, etc.) que seus campos podem assumir. Esse conjunto de valores é denominado domínio do campo. Além disso, devemos também indicar se o campo pode aceitar valores vazios (null) ou não. As colunas que não podem aceitar valores vazios são chamadas de obrigatórias, enquanto as que aceitam são chamadas de opcionais. 

O domínio sempre terá uma descrição física, como por exemplo, o tipo de dado que cada atributo comportará. O domínio poderá ter também uma descrição semântica. Essa descrição é mais conceitual e serve como complemento da descrição física, podendo detalhar os dados e informações a respeito do atributo. 

**OBS:** Geralmente, os SGBD exigem que todas as chaves primárias sejam obrigatórias. O mesmo não acontece para as chaves estrangeiras.

## Restrições de integridade

> Regras de negócio: São regras que garantem a integridade e o funcionamento de uma organização.

Um dos principais motivos de um SGBD é manter a integridade dos dados. Dizer que um dado é íntegro é dizer que ele reflete a corretamente realidade representada pelo banco de dados, e que os dados sejam consistentes entre si. Ou seja, se os dados obedecerem certa lógica definida pelo SGBD, e se as restrições semânticas estiverem sendo levadas em consideração, o dado será íntegro. 

O SGBD utiliza regras que irão definir se um dado está, ou não, de acordo com as regras de integridade do sistema. Essas regras podem ser as seguintes:

- **Integridade de Domínio**:  **As restrições deste tipo verificam se os dados inseridos estão de acordo com o tipo de dado definido para aquele atributo.
- **Integridade de Vazio**: As restrições desse tipo verificam se os atributos são obrigatórios e opcionais, e garantem que os dados estejam seguindo a lógica corretamente.
- **Integridade de Chave:** Trata-se de restrições que define que os valores das chaves primárias e alternativas não possam ser nulos.
- **Integridade Referencial:** É a restrição que define que os valores dos campos de chaves estrangeiras precisam existir nas tabelas referenciadas pela chave primária.

Além das restrições acima, há também restrições que não estão listadas, mas que garantem a integridade dos dados. Essa restrição é chamada de *restrição semântica*, e esta relacionada com as regras do negócio do banco de dados. Essas restrições não podem ser tratadas diretamente pelo SGBD, portanto, é necessário definir as restrições em tempo de execução, onde essas restrições serão baseadas nas regras que os atributos devem possuir.

***

# Especificação de banco de dados relacional

>Schema de um banco de dados é estrutura que define a organização e a estrutura lógica dos dados armazenados no sistema.

Um banco de dados relacional deve ter no mínimo a definição do seguinte:

- Tabelas que formam o banco de dados
- Colunas que as tabelas possuem
- Restrições de integridade

A representação da tabela de um banco de dados é definida por: NomeTabela (**Atributo1**, Atributo2, Atributo 3…). O atributo que está sublinhado representa a chave primária da tabela. Para utilizarmos chaves estrangeiras precisamos indicar qual tabela ela referencia. Por exemplo, considere o exemplo abaixo:

```
Emp(CodEmp, NomeEmp, CodDept, CategFunc, CIC)
CodDept referencia Dept
Dept (CodDept, NomeDep)
```

**OBS**: Para referenciar a múltiplas chaves primárias utilizamos (chave1, chave2) referenciam Tabela.

