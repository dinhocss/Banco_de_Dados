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

