> O termo engenharia reversa vem do fato de usar-se como ponto de partida do processo um modelo já implementado para obter sua especificação (modelo conceitual) 

# Engenharia Reversa de Modelos Relacionais

No caso de um banco de dados, a engenharia reversa ocorre quando transformamos modelos mais ricos em detalhes de implementação em modelos mais abstratos. Ao tratarmos de engenharia reversa de modelos relacionais temos como ponto de partida o modelo lógico do banco de dados sendo transformado num modelo conceitural. 

O processo de engenharia reversa de um modelo relacional segue os seguintes passos:
1. Construção do modelo ER correspondente a cada tabela.
2. Definição de relacionamentos 1:n e 1:n.
3. Definição de atributos
4. Definição de identificadores de entidade e relacionamento

Para exemplificar o processo de engenharia reversa vamos dar um exemplo, onde parte-se de um modelo lógico, transformando-o em um modelo conceitual. O modelo lógico abaixo refere-se a um banco de dados de um sistema acadêmico, cujo o esquema é representado abaixo:

Disciplina(**CodDisciplina**, NomeDisc )
Curso(**CodCr**, NomeCr)
Curric(**CodCr, CodDisc**, Obr/Opc)
	CodCr referencia Curso
	CodDisc referencia Disciplina
Sala(**CodPr, CodSl**, Capacidade)
	CodPr referencia Predio
Predio(**CodPr**, Endereço)
Turma(**Anosem, CodDisc,SiglaTur**, Capacidade, CodPr, CodSl)
	CodDisc referencia Disciplina
	(CodPr, CodSl) referencia Sala
Laboratório(**CodPr, CodSl**, Equipam)
	(CodPr,CodSl) referencia Sala

A partir desse esquema lógico vamos abordar o passo a passo para transformá-lo em um modelo conceitual.

## Identificação da construção ER correspondente a cada tabela

Na primeira etapa da engenharia reversa de um modelo relacional verificamos para cada tabela do modelo relacional, qual construção é correspondente em relação ao modelo ER. Uma tabela pode corresponder a:
* Uma entidade
* Um relacionamento n:n
* Uma entidade especializada

O fator determinante para verificarmos a relação entre a tabela em questão com seu correspondente do modelo ER é através da composição de sua chave primária. Tabelas podem ser classificadas em três tipos de acordo com a composição de sua chave primária, sendo elas:
* **Regra 1:** *Chave primária composta por mais de uma chave estrangeira*
	As tabelas que possuem chave primária composta por mais de uma chave estrangeira implementa um relacionamento N:N entre as entidades correspondentes. Por exemplo, no esquema mostrado acima a tabela *Curric* possui como chave primária as chaves estrangeiras *CodCr* e *CodDisc*, que referenciam *Curso* e *Disciplina* respectivamente. Portanto, o correspondente desta tabela no modelo ER será um **relacionamento N:N**.
* **Regra 2:** *Toda chave primária é uma chave estrangeira*
	A tabela cuja chave primária é toda ela uma chave estrangeira representa uma entidade que forma uma especialização da entidade correspondente à tabela referenciada pela chave estrangeira. No esquema acima temos a tabela *Laboratório* que possui  como chave primária as chaves estrangeiras *CodPr* e *CodSl*. Note que a chave primária de Laboratório não possui nenhuma chave própria. Ambas as chaves são estrangeiras, portanto, isso configura que Laboratório é uma especialização de Sala, indicando que haverá um registro de laboratório somente se houver um regristro de Sala.
* **Regra 3:** *Demais casos*
	Quando a tabela em questão não possuir como chave primária duas chaves estrangeiras (regra 1) ou quando a chave primária não for totalmente composta por chaves estrangeiras (regra 2), esta tabela será representada como uma entidade. 

Após termos feito a classificação das tabelas em relação as suas entidades ou relacionamentos, é possível montar um diagrama ER inicial, por exemplo:
![image](https://github.com/user-attachments/assets/99e9838e-6a9d-4dfb-92c7-85f199fee828)

## Definição de Relacionamentos 1:n e 1:1

Toda chave estrangeira que não corresponde a um relacionamento N:N nem a uma entidade especializada possui relacionamento ou 1:n ou 1:1. Não há regras para definir relacionamentos 1:n e 1:1. Para isso, precisamos analisar os possíveis conteúdos do banco de dados. No caso do exemplo dado acima, os relacionamentos 1:n e 1:1 são definidos nas tabelas *Sala* e *Turma*, portanto, teríamos:
![image](https://github.com/user-attachments/assets/430c5057-6921-4e3b-95f3-91f64b8374a0)

## Definição de atributos

Nesta etapa definimos os nomes de todos os atributos que não são chaves estrangeiras. É necessário observar que as chaves estrangeiras não são atributos num diagrama ER. Isto ocorre pois essas chaves são representadas por relacionamentos, e eles já são implementados no diagrama ER. Portanto, a nomeação dos atributos pode ser feita da seguinte maneira:
![image](https://github.com/user-attachments/assets/a967574e-c8b8-456f-a77f-39361c87b479)

## Definição de identificadores de entidades

No último passo, são definidos os identificadores das entidades e dos relacionamentos. A regra para definição dos identificadores é a seguinte:
* *Coluna da chave primária que não é chave estrangeira*
	Toda coluna que é chave primária e não é chave estrangeira de outra entidade corresponde a  um atributo identificador da entidade ou relacionamento.
* *Coluna da chave primária que é chave estrangeira*
	Toda coluna que faz parte da chave primária e que é chave estrangeira corresponde a um identificador externo da entidade. Por exemplo, a tabela *Turma* possui como identificador (anoSem, siglaTur e codDisc). Repare que codDisc além de ser chave primária de *Turma*, também é chave estrangeira da entidade *Disciplina*. Portanto, a entidade *Turma* é identificada também pelo relacionamento com disciplina. 

Executando este último passo para a engenharia reversa temos o seguinte diagrama ER:
![image](https://github.com/user-attachments/assets/e0a13893-4b86-4091-8732-a46b2cf77679)

