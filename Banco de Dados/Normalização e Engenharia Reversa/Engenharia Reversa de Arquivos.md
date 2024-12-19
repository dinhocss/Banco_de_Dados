> Este processo permite obter um modelo lógico relacional a partir de um modelo lógico de um banco de dados não relacional.

# Visão geral do processo de engenharia reversa 

O processo inicia-se a partir das descrições dos arquivos que compõem o sistema existente. O objetivo é extrair informações úteis desses arquivos e transformá-los em um modelo relacional. O primeiro passo é transformar os arquivos em um modelo relacional não normalizado.

**OBS**: O tipo de arquivo pode ser qualquer um, como CSV, arquivo binário, arquivo texto, entre outros. 

Após termos o modelo relacional não normalizado, provavelmente teremos redundâncias, portanto, aplica-se o processo de normalização para eliminar essas redundâncias e obter um modelo mais confiável. 

Depois que os arquivos são normalizados, o próximo passo é **integrar os diferentes modelos relacionais gerados**. Essa integração consiste em:
* **Identificar duplicidades**: Atributos ou dados comuns entre tabelas diferentes são identificados.
* **Unificar informações:** Esses dados duplicados são representados apenas uma vez no esquema relacional final.
Esse processo é essencial para garantirmos a integridade do esquema relacional, pois eliminamos as informações redundantes, melhorando o desempenho do banco de dados.

Por último, após obtermos o esquema relacional completo, podemos transformá-lo em um diagrama ER. Esse processo é descrito [aqui](https://github.com/dinhocss/Banco_de_Dados/blob/182ba17074e19609e5680d5d61a7eaccd312a68a/Banco%20de%20Dados/Normaliza%C3%A7%C3%A3o%20e%20Engenharia%20Reversa/Engenharia%20Reversa%20de%20Modelos%20Relacionais.md).

# Exemplificando a partir de um documento

Considere um documento que representa um sistema de gerência de projetos. Cada projeto é identificado por um código, uma descrição e o tipo de projeto. E cada projeto possui os empregados que estão relacionados a eles. Já para cada empregado tempos o código, nome, salário, categoria, data do inicio no projeto e o tempo alocado no projeto. A figura abaixo representa esse documento:
![image](https://github.com/user-attachments/assets/41b28106-ac79-4ca2-ab40-fd7eda3b962f)

## Representação na forma de tabela não normalizada

O primeiro passo é transformar os dados contidos no arquivo a ser normalizado em um esquema relacional. A tabela não normalizada referente  ao documento apresentado acima é representada abaixo:
![image](https://github.com/user-attachments/assets/e1463340-f943-4385-b383-30c5279084f1)

Essa tabela é dita não normalizada pois possui uma tabela aninhada. Uma tabela é dita aninhada se a coluna conter valores multi-valorados ao invés de valores atômicos. A tabela acima pode ser escrita através do seguinte esquema relacional:
Proj(**CodProj**, Tipo, Descr
				(**CodEmp**, Nome, Cat, Sal, DataIni, TempAl))
No exemplo acima utilizamos parênteses aninhados que representam tabelas aninhadas.
# Normalização

Após obtermos o esquema relacional referente a um documento, aplicamos o processo de normalização a este esquema. Este processo baseia-se no conceito de *forma normal*. Uma forma normal é uma regra que deve ser obedecida por uma tabela para que ela seja considerada "bem projetada".

Há diversas formas normais que verificam uma tabela relacional. Serão vistas aqui as quatro primeiras, chamadas de primeira, segunda, terceira e quarta forma normal, sendo representadas por *1FN*, *2FN*, *3FN* e *4FN* respectivamente.

## Passagem à primeira forma normal (1FN)

O próximo passo da normalização consta na transformação de um esquema relacional não normalizado em um esquema relacional na primeira forma normal. O objetivo da primeira forma normal é **eliminar as tabelas aninhadas**. Para eliminarmos as tabelas aninhadas podemos levar em consideração duas maneiras:
* *Utilizar uma única tabela representando a primeira forma normal*
	Neste caso, cria-se uma tabela que inclui redundâncias e leva em consideração todos os atributos da tabela não normalizada. Por exemplo, considere o exemplo anterior, onde tinhamos Proj(**CodProj**, Tipo, Descr
				(**CodEmp**, Nome, Cat, Sal, DataIni, TempAl)).
	A tabela referente a esse esquema relacional seria: Proj(CodProj, Tipo, Desc, CodEmp, Nome, Cat, Sal, DataIni, TempAl).
* *Utilizar uma tabela para cada tabela aninhada*
	Este é o caso que será utilizado daqui em diante, e envolve criar uma tabela para cada tabela aninhada. Levando em consideração o exemplo do Projeto teríamos:
		Proj(**CodProj**, Tipo, Descr)
		ProjEmp(**CodProj**, **CodEmp**, Nome, Cat, Sal, DataIni, TempAl)

A passagem à primeira forma normal via decomposição de tabelas é feita nos seguintes passos:
1. Cria-se uma tabela referente a tabela não normalizada que contém apenas valores atômicos, ou seja, sem levar em consideração as tabelas aninhadas.
2. Para cada tabela aninhada, é criada uma tabela na 1FN com os seguintes atributos:
	* A chave primária de cada uma das tabelas que a tabela em questão está aninhada
	* As colunas da própria tabela aninhada.
3. São definidas as chaves primárias das tabelas associadas as tabelas aninhadas.

Tomando o exemplo visto acima referente as tabelas *Proj* e *ProjEmp*, vamos analisar a tabela *ProjEmp*. Primeiramente temos a chave primária referente a tabela externa na forma não normalizada, que é *CodProj*. E em seguida temos os atributos referentes aos atributos da tabela aninhada em questão. Observe também que tanto *codProj* quanto *codEmp* são chaves primárias em relação a ProjEmp. Isto ocorre pois um mesmo empregado pode trabalhar em mais de um projeto, portanto, para evitar inconsistência de integridade, precisamos ter as chaves *codProj* e *CodEmp* como chaves primárias.

Segue abaixo um exemplo visual referente as tabelas após a 1FN:
![image](https://github.com/user-attachments/assets/dc57a41a-ecf1-4c97-813f-6b6ab4a5526b)

**OBS:** Caso o empregado pudesse participar de apenas um projeto, a chave primária de *ProjEmp* seria unicamente *CodEmp*. 

**OBS II:** Por hora, o nome das tabelas não é importante, portanto recomenda-se nomear as tabelas somente após o processo de normalização.

Considere um segundo exemplo de um esquema relacional da forma não normalizada:
Arq-Alunos(**CodAl**, NomeAl,
		(**CodCurso**, SemIngresso)
		(**CodDisc**,
			(**SemDisCursada**, NotaDisc)))
Como a tabela não normalizada possui três tabelas aninhadas, a 1FN gerará quatro tabelas. As tabelas resultantes da 1FN em relação a uma tabela não normalizada é dada por:
Aluno(**CodAl,** NomeAl)
AlunoCurso (**CodAl**, **CodCurso**, SemIngresso)
AlunoDisc(**CodAl**, **CodDisc**)
DiscSem(**CodAl**, **CodDisc**, **SemDisCursada**, NotaDisc)

Note que a primeira tabela é referente a tabela não normalizada sem considerar as tabelas aninhadas. A segunda tabela possui além do seu identificador, o identificador da tabela externa correspondente a forma não normalizada. Levando em conta o mesmo princípio, a tabela *DiscSem* possui como chave primária tanto *CodAl* quanto *CodDisc*, que fazem parte de tabelas externas em relação a forma não normalizada.

**OBS:** Apesar dos exemplos acima mostrar chaves primárias sendo a concatenação das chaves externas das tabelas aninhadas correspondentes, pode haver o caso de a chave primária não incluir a chave primária da tabela externa. 

## Dependência funcional

Para entendermos as formas normais 2FN e 3FN é necessário entender o conceito de *dependência funcional*. Considere a imagem a seguir:
![image](https://github.com/user-attachments/assets/e4c32aca-c41a-4d57-8c6b-e7678e201f9a)

