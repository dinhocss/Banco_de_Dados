# Álgebra Relacional

>Tanto a álgebra relacional quanto o cálculo relacional são linguagens formais que definem um conjunto de regras a serem implementadas quando desejamos realizar operações em cima de dados ou tabelas.

A álgebra relacional nos fornece um conjunto de operações feitas em cima de um modelo relacional. Essas operações permitem que o usuário possa recuperar informações e manipular os dados recebidos, criando uma nova tabela referente a operação feita. A nova tabela pode realizar as mesmas operações, criando outras novas tabelas. Essa sequência de operações algébricas são chamadas de *expressão da álgebra relacional*.

🎯[A importância da Algebra Relacional]()

Essas operações que podem ser realizadas pela álgebra relacional podem ser divididas em dois grupos. Um grupo inclui as operações que podem ser realizadas em cima de um conjunto matemático. Isto ocorre porque, de acordo com o modelo formal, uma tabela é um conjunto de tuplas. Essas operações são UNIÃO, INTERSECÇÃO, DIFERENÇA, PRODUTO CARTESIANO. O outro grupo consta com operações desenvolvidas especificamente para bancos de dados relacionais, entre eles temos SELEÇÃO, JUNÇÃO e PROJEÇÃO.

## Operações de Seleção

A operação de **seleção** em álgebra relacional funciona como um **filtro** para as tabelas, retornando apenas as **linhas desejadas** com base nas condições especificadas. Essa operação é fundamental para filtrar dados de acordo com critérios específicos e é uma das operações básicas da álgebra relacional.

### Características da Operação de Seleção

- **Notação**: A operação de seleção é representada pelo símbolo **σ** (sigma).
    - A notação para a operação de seleção é:  
      `σ_{condição}(R)`  
      Onde:
        - **R** é a tabela ou relação sobre a qual a operação é aplicada.
        - **condição** é a expressão booleana que define os critérios para a seleção das linhas.

- **Condições**: As condições passadas para a operação de seleção são expressões **booleanas**. Elas podem incluir:
    - Comparações (ex: `idade > 18`)
    - Operadores lógicos como **AND**, **OR** e **NOT**.

- **Resultado**: A operação de seleção retorna uma nova tabela que contém apenas as linhas que **satisfazem** as condições especificadas.

- **Junção de Condições**: Podemos combinar múltiplas condições em uma única operação de seleção utilizando os operadores lógicos:
    - **AND**: Para garantir que todas as condições sejam verdadeiras.
    - **OR**: Para garantir que ao menos uma das condições seja verdadeira.
    - **NOT**: Para excluir condições específicas.

- **Ordem de Aplicação**: A operação de seleção é **comutativa**. Isso significa que a ordem das condições não altera o resultado da operação.  
    - Exemplo:  
      `σ_{condição1}(σ_{condição2}(R)) = σ_{condição2}(σ_{condição1}(R))`

### Exemplo em SQL

Em SQL, a operação de seleção é realizada com a cláusula `WHERE` em uma consulta `SELECT`. Veja um exemplo prático de como isso é feito:

```
sql
SELECT Nome, Idade
FROM Pessoas
WHERE Idade > 18 AND Cidade = 'São Paulo';
```

Esse exemplo seleciona os nomes e idades de pessoas que têm mais de 18 anos e moram em São Paulo. Abaixo está uma representação simplificada da operação de seleção aplicada a uma tabela:
Tabela **(Pessoas)**
|Pessoa_ID|Nome|Idade|Cidade|
|---------|----|-----|------|
|1        |João|31   |Rio de Janeiro|
|2        |Patricia|29|São Paulo|
|3        |Pedro|35|Rio Grande do Sul|
|4        |Alan|28|Bahia|
|5        |Aline|30|Amazonas|

Aplicando **σIdade>28 ^ Cidade = 'São Paulo'**. A tabela resultante é:
|Pessoa_ID|Nome|Idade|Cidade|
|---|---|---|---|
2|Patricia|29|São Paulo|

Neste caso, a seleção resultou em uma nova tabela contendo apenas as pessoas com idade superior a 18 e morando em São Paulo.

### Resumo
A operação de seleção é um filtro poderoso e flexível que permite escolher quais linhas de uma tabela serão mantidas em um resultado. É fundamental na álgebra relacional e é comumente usada em consultas SQL para restringir os dados retornados.

### Pontos-chave:
**Símbolo de Seleção**: σ

**Condições**: São expressões booleanas (ex: idade > 18).

**Comutatividade**: A ordem das seleções não altera o resultado.

**Junção de Condições**: Usando AND, OR e NOT.

**Resultado**: Uma nova tabela com as linhas filtradas.

## Operações de Projeção

A operação de **projeção** em álgebra relacional permite selecionar **colunas específicas** (ou atributos) de uma tabela, retornando uma nova tabela com apenas esses atributos desejados. A projeção é útil para focar em informações específicas sem modificar as linhas da tabela original.

### Características da Operação de Projeção

- **Notação**: A projeção é representada pelo símbolo **π** (pi).
    - Notação:  
      `π_{Atributos}(Tabela)`  
      Onde:
        - **Atributos** são os nomes das colunas a serem incluídas na tabela resultante.
        - **Tabela** é a relação de entrada.

- **Parâmetros**: Na projeção, passamos os **nomes dos atributos** que desejamos na tabela resultante. Apenas as colunas especificadas serão incluídas no resultado.

- **Resultado**: A operação retorna uma nova tabela contendo apenas os atributos especificados, mas preserva todas as linhas da tabela original. Os atributos aparecem na mesma ordem que na tabela de entrada.

- **Ordem de Aplicação**: A operação de projeção é **não comutativa**. Isso significa que a ordem dos atributos na projeção importa, e mudá-la pode alterar o resultado final.

- **Remoção de Tuplas Repetidas**: Em uma projeção, as **tuplas duplicadas** são automaticamente removidas. Para isso, o sistema de gerenciamento de banco de dados pode aplicar técnicas como **classificação** (sorting) ou outras abordagens para identificar e eliminar duplicatas, o que pode aumentar o tempo de processamento.

### Observação

- O número de linhas na tabela resultante será sempre **≤** o número de linhas na tabela original, pois as duplicatas são descartadas.

### Exemplo em SQL

Em SQL, a projeção é realizada com o comando `SELECT`, especificando as colunas que desejamos incluir. Veja um exemplo prático:

```
sql
SELECT Nome, Idade
FROM Pessoas;
```

Esse exemplo seleciona apenas os atributos Nome e Idade da tabela Pessoas, ignorando todos os demais atributos. Abaixo, apresentamos uma representação visual de uma operação de projeção aplicada a uma tabela.

Tabela **(Pessoas)**
|Pessoa_ID|Nome|Idade|Cidade|
|---------|----|-----|------|
|1        |João|31   |Rio de Janeiro|
|2        |Patricia|29|São Paulo|
|3        |Pedro|35|Rio Grande do Sul|
|4        |Alan|28|Bahia|
|5        |Aline|30|Amazonas|

Aplicando **πNome,Idade**. A tabela resultante é:
|Nome|Idade|
|---|---|
|João|31|
|Patricia|29|
|Pedro|35|
|Alan|28|
|Aline|30|

Neste exemplo, a projeção resulta em uma nova tabela com apenas os atributos Nome e Idade, preservando todas as linhas da tabela original e removendo quaisquer colunas não especificadas.

### Resumo
A operação de projeção é ideal para selecionar colunas específicas de uma tabela, permitindo uma visão focada nos atributos desejados sem modificar o conjunto de linhas. É amplamente utilizada para simplificar a visualização de dados e remover informações desnecessárias.

### Pontos-chave:
**Símbolo de Projeção**: π

**Parâmetros**: Nomes dos atributos desejados.

**Remoção de Duplicatas**: Tuplas duplicadas são descartadas automaticamente.

**Ordem de Atributos**: A operação é não comutativa.

**Resultado**: Tabela com apenas as colunas projetadas.

## Operação de Renomeação
A operação de renomeação é dada pelo símbolo **ρ**, e é utilizada para renomear colunas ou nomes de tabelas. 

### Características da operação de Renomeação

- **Notação**: A renomeação é representada pelo símbolo **ρ**.
    - Notação:  
      `ρNovaTabela (TabelaAntiga)`  

- **Parâmetros**: Na renomeação os parâmetros são a tabela que se deseja renomear e o nome da tabela desejada.

- **Resultado**: A operação retorna a tabela com o nome desejado.

## Diferentes Tipos de Junção
As operações de **junção** são fundamentais na álgebra relacional, permitindo combinar dados de duas tabelas com base em uma condição. As junções são úteis para relacionar tabelas em um banco de dados relacional e extrair informações combinadas.

Existem vários tipos de junções, cada um adequado para diferentes situações e necessidades de filtragem de dados.

### Tipos de Junções

#### 1. Junção Natural (Natural Join)

A **junção natural** combina duas tabelas com base em colunas que possuem o mesmo nome e valores equivalentes. Ela elimina automaticamente as colunas duplicadas na tabela resultante.

##### Notação
- Notação: `R ⋈ S`
  - Onde `R` e `S` são as tabelas a serem combinadas.

##### Exemplo

Suponha as tabelas `Funcionários` e `Departamentos`:

**Tabela Funcionários**

| FuncID | Nome       | DeptID |
|--------|------------|--------|
| 1      | João       | 10     |
| 2      | Maria      | 20     |
| 3      | Pedro      | 10     |

**Tabela Departamentos**

| DeptID | DeptNome       |
|--------|-----------------|
| 10     | Recursos Humanos |
| 20     | TI               |

**Junção Natural (Funcionários ⋈ Departamentos)**

| FuncID | Nome   | DeptID | DeptNome          |
|--------|--------|--------|-------------------|
| 1      | João   | 10     | Recursos Humanos  |
| 2      | Maria  | 20     | TI                |
| 3      | Pedro  | 10     | Recursos Humanos  |

#### 2. Junção Theta (θ-Join)

A **junção theta** permite combinar tabelas com uma condição genérica (θ), como `=`, `>`, `<`, `>=`, `<=`, etc., entre colunas das tabelas.

##### Notação
- Notação: `R ⋈_{θ} S`
  - Onde `θ` é uma condição lógica.

##### Exemplo

Para uma junção onde `FuncID > DeptID`:

**Junção Theta (Funcionários ⋈_{FuncID > DeptID} Departamentos)**

| FuncID | Nome   | DeptID | DeptNome         |
|--------|--------|--------|------------------|
| 2      | Maria  | 1      | Recursos Humanos |
| 3      | Pedro  | 2      | TI               |

#### 3. Semi-Junção

A **semi-junção** combina duas tabelas como uma junção, mas só retorna as colunas da primeira tabela (`R`). É útil para verificar a existência de correspondências.

##### Notação
- Notação: `R ⋉ S`

##### Exemplo

Aplicando uma semi-junção para encontrar funcionários que estão associados a um departamento.

**Semi-Junção (Funcionários ⋉ Departamentos)**

| FuncID | Nome   | DeptID |
|--------|--------|--------|
| 1      | João   | 10     |
| 2      | Maria  | 20     |
| 3      | Pedro  | 10     |

#### 4. Junção Externa (Outer Join)

A **junção externa** retorna todas as tuplas correspondentes, mais aquelas que não possuem correspondência, preenchendo com valores nulos (`NULL`) para as colunas sem correspondência.

##### Notação
- Notação: `R ⟗ S`

#### 4.1. Junção Externa Esquerda (Left Outer Join)

Retorna todas as tuplas da **primeira tabela (R)**, incluindo as que não possuem correspondência na segunda tabela (S), preenchendo com `NULL` onde não há correspondência.

##### Notação
- Notação: `R ⟕ S`

##### Exemplo

**Junção Externa Esquerda (Funcionários ⟕ Departamentos)**

| FuncID | Nome   | DeptID | DeptNome         |
|--------|--------|--------|------------------|
| 1      | João   | 10     | Recursos Humanos |
| 2      | Maria  | 20     | TI               |
| 3      | Pedro  | 10     | Recursos Humanos |
| 4      | Carla  | 30     | NULL             |

#### 4.2. Junção Externa Direita (Right Outer Join)

Retorna todas as tuplas da **segunda tabela (S)**, incluindo aquelas sem correspondência na primeira tabela (R), preenchendo com `NULL` onde não há correspondência.

##### Notação
- Notação: `R ⟖ S`

##### Exemplo

**Junção Externa Direita (Funcionários ⟖ Departamentos)**

| FuncID | Nome   | DeptID | DeptNome         |
|--------|--------|--------|------------------|
| 1      | João   | 10     | Recursos Humanos |
| 2      | Maria  | 20     | TI               |
| NULL   | NULL   | 40     | Marketing        |

#### 4.3. Junção Externa Integral (Full Outer Join)

Retorna todas as tuplas das duas tabelas, preenchendo com `NULL` onde não houver correspondência em nenhuma das tabelas.

##### Notação
- Notação: `R ⟗ S`

##### Exemplo

**Junção Externa Integral (Funcionários ⟗ Departamentos)**

| FuncID | Nome   | DeptID | DeptNome         |
|--------|--------|--------|------------------|
| 1      | João   | 10     | Recursos Humanos |
| 2      | Maria  | 20     | TI               |
| 3      | Pedro  | 10     | Recursos Humanos |
| 4      | Carla  | 30     | NULL             |
| NULL   | NULL   | 40     | Marketing        |

### Resumo das Junções

| Tipo de Junção       | Descrição                                                                                       |
|----------------------|-------------------------------------------------------------------------------------------------|
| Junção Natural       | Combina tabelas com base em colunas com o mesmo nome, sem duplicar as colunas correspondentes.  |
| Junção Theta         | Permite combinações baseadas em condições específicas entre as tabelas.                         |
| Semi-Junção          | Similar a uma junção, mas retorna apenas colunas da primeira tabela.                           |
| Junção Externa Esquerda   | Retorna todas as tuplas da primeira tabela, mesmo as que não possuem correspondência.         |
| Junção Externa Direita    | Retorna todas as tuplas da segunda tabela, mesmo as que não possuem correspondência.          |
| Junção Externa Integral   | Retorna todas as tuplas de ambas as tabelas, preenchendo com `NULL` onde não há correspondência.|

***

## União, Intersecção e Diferença

Várias operações de teoria de conjuntos podem ser aplicadas para mesclar informações sobre duas relações, como *união*, *intersecção* e *diferença*. Essas três operações possuem alguns elementos em comum, como por exemplo:
Sendo R e S conjuntos que representam duas relações, para realizarmos operações de conjuntos sobre essas relações precisamos do seguinte:
- R e S precisam ter o mesmo número de atributos.
- Os domínios dos atributos devem ser compatíveis entre si.
- Os schemas de R e S devem ser compatíveis, ou seja, o mesmo número de atributos, com o mesmo tipo na mesma ordem.
- A *união* é dada por R∪S, e contem todos os elementos que estão em R ou S.
- A *intersecção* é dada por R∩S, e contém todos os elementos que estão em R e S.
- A *diferença* é dada por R-S, e contém todos os elementos que estão em R, mas não estão em S.

  ## Produto cartesiano

É uma operação binária, ou seja, é o produto de duas tabelas. A notação é dada por RxS, e nos fornece a combinação de todos os elementos de R com todos os elementos de S. Esta operação serve como base para as operações de junção, pois é uma maneira de relacionar duas tabelas e exibí-las em uma única tabela. 

Diferenta das operações de União, Intersecção e Diferença,os schemas entre as tabelas podem ser diferentes.

***

## Resumo geral

|Operação|Resultado|Como utilizar|
|---|---|---|
|σ (Seleção)|Uma tabela com as tuplas resultantes de uma condição booleana|σBugdet < 100000 ^ ReleaseDate = 2000 (Movies)|
|π(Projeção)|Uma tabela com os atributos desejados, contendo o mesmo número de registros da tabela original|πTitle, Distribution(Movies)|
| ⋈ (Junção Natural)         | Combina tuplas de duas relações que possuem valores iguais nos atributos comuns                            | `R ⋈ S`                                                         |
| ⋈θ (Junção Theta)          | Combina tuplas de duas relações que atendem a uma condição específica, podendo incluir operadores como `=`, `<`, `>` | `R ⋈_{R.A = S.B} S`                                            |
| ⋉ (Semi-junção)            | Retorna apenas as tuplas de `R` que possuem correspondência com `S` em uma condição especificada           | `R ⋉_{R.A = S.B} S`                                            |
| ⟕ (Junção Externa Esquerda)| Inclui todas as tuplas de `R` e as correspondentes de `S`, com `NULL` para valores ausentes de `S`         | `R ⟕ S`                                                         |
| ⟖ (Junção Externa Direita) | Inclui todas as tuplas de `S` e as correspondentes de `R`, com `NULL` para valores ausentes de `R`         | `R ⟖ S`                                                         |
| ⟗ (Junção Externa Integral)| Inclui todas as tuplas de `R` e `S`, com `NULL` para valores ausentes de qualquer uma das relações         | `R ⟗ S`                                                         |
| ∪ (União)                  | Combina todas as tuplas de `R` e `S`, sem duplicações, desde que `R` e `S` tenham o mesmo esquema          | `R ∪ S`                                                         |
| ∩ (Intersecção)            | Retorna as tuplas comuns a `R` e `S`                                                                       | `R ∩ S`                                                         |
| - (Diferença)              | Retorna as tuplas que estão em `R` mas não em `S`                                                          | `R - S`                                                         |
| × (Produto Cartesiano)     | Combina todas as tuplas de `R` com todas as tuplas de `S`, formando pares                                 | `R × S`                                                         |
| ÷ (Divisão)                | Retorna as tuplas de `R` que têm correspondência com todas as tuplas de `S` em um subconjunto de atributos | `R ÷ S`                                                         |
