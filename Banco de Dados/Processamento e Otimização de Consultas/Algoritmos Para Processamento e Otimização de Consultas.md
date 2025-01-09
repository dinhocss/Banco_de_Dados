Esta seção irá abordar o modo que o SGBD utiliza para processar, otimizar e executar consultas de alto nível. A primeira fase de uma consulta é a leitura, análise e validação da consulta. Após analisada, essa consulta é transformada em uma representação interna, que é mais fácil de manipular, podendo ser uma *árvore de consulta* ou um *grafo de consulta*. Por último é realizado um planejamento e otimização da consulta, onde o SGBD determina a melhor maneira da consulta ser realizada.

## Como o SGBD lida com uma consulta SQL

Como dito anteriormente, quando uma consulta SQL é realizada, o SGBD verifica a integridade dos dados. Ele faz isso através da leitura, análise e validação da consulta. Segue abaixo o modo como é feito essa leitura pelo SQL:
* **Varredura:** O SGBD realiza a leitura da consulta e identifica seus tokens, que são palavras-chave existentes na consulta, como:
	* Palavras-chave SQL (SELECT, FROM, WHERE)
	* Nomes de tabelas e colunas
	* Operadores como <, = e >
* **Analisador Sintático:** O SGBD verifica se a estrutura da consulta está de acordo com as regras de sintaxe SQL, como:
	* SELECT nome, idade FROM usuarios - Consulta correta
	* SELECT nome idade FROM usuarios - Consulta incorreta (faltou uma vírgula)
* **Validação:** O SGBD verifica se os elementos da consulta existem no banco de dados, como:
	* Os nomes de tabelas e atributos existem no banco de dados?
	* As operações são válidas no esquema de banco de dados?

Após ser feita a verificação da integridade dos dados, a consulta é passada para uma representação interna, que facilita a manipulação. Essa representação pode ser dada de duas formas:
* **Árvore de consulta**: Uma estrutura de dados em forma de árvore, que reflete as operações de consulta, como por exemplo:
	* A raiz da árvore pode ser a palavra-chave *SELECT*
	* Os nós intermediários podem representar operações como *WHERE* e *FROM*
	* As folhas representam as tabelas e colunas envolvidas
* **Grafo de consulta:** Outra forma de representar consultas, sendo mais utilizado para consultas mais complexas, na qual há várias tabelas e colunas envolvidas.

Por último é feito um planejamento e otimização das consultas. Aqui é onde o SGBD irá verificar a maneira mais otimizada para realizar as consultas, onde é utilizada as seguintes estratégias:
* **Estratégias de execução**: O SGBD avalia como os dados podem ser recuperados de maneira mais eficiente, onde há a seguinte análise:
	* Quais índices estão disponíveis?
	* Qual a ordem de junção mais rápida?
	* É mais eficiente filtrar primeiro ou fazer uma junção?
* **Otimzação de consulta:** Nessa parte, o SGBD avalia a maneira mais otimizada de realizar a consulta, com intuito de diminuir o tempo de execução e o uso de recursos, por exemplo:
	* Escolher um índice ao invés de percorrer a tabela inteira
	* Reorganizar a ordem das operações

Segue abaixo um esquema de como é feito essa análise referente a uma consulta:
![image](https://github.com/user-attachments/assets/3765882e-9bf5-4419-a686-4a87a23f5b77)
