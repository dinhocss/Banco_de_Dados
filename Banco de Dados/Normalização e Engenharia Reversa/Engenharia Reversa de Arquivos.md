> Este processo permite obter um modelo lógico relacional a partir de um modelo lógico de um banco de dados não relacional.

# Visão geral do processo de engenharia reversa 

O processo inicia-se a partir das descrições dos arquivos que compõem o sistema existente. O objetivo é extrair informações úteis desses arquivos e transformá-los em um modelo relacional. O primeiro passo é transformar os arquivos em um modelo relacional não normalizado.

**OBS**: O tipo de arquivo pode ser qualquer um, como CSV, arquivo binário, arquivo texto, entre outros. 

Após termos o modelo relacional não normalizado, provavelmente teremos redundâncias, portanto, aplica-se o processo de normalização para eliminar essas redundâncias e obter um modelo mais confiável. 

Depois que os arquivos são normalizados, o próximo passo é **integrar os diferentes modelos relacionais gerados**. Essa integração consiste em:
* **Identificar duplicidades**: Atributos ou dados comuns entre tabelas diferentes são identificados.
* **Unificar informações:** Esses dados duplicados são representados apenas uma vez no esquema relacional final.
Esse processo é essencial para garantirmos a integridade do esquema relacional, pois eliminamos as informações redundantes, melhorando o desempenho do banco de dados.

Por último, após obtermos o esquema relacional completo, podemos transformá-lo em um diagrama ER. Esse processo é descrito [aqui]().

