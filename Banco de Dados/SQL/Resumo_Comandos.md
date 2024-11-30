## Comandos DDL

| Comando          | O que faz                                  | Como utilizar                                  |
| ---------------- | ------------------------------------------ | ---------------------------------------------- |
| CREATE SCHEMA    | Cria um novo esquema                       | CREATE SCHEMA financeiro;                      |
| DROP SCHEMA      | Remove um schema existente                 | DROP SCHEMA financeiro;                        |
| CREATE TABLE | Cria uma nova tabela                       | CREATE TABLE Funcionarios()                    |
| ALTER TABLE | Modifica atributos de uma tabela existente | ALTER TABLE Funcionarios ADD COLUMN Idade INT; |
| DROP TABLE       | Remove uma tabela existente                | DROP TABLE Funcionarios                        |

---
## Comandos DML

| Comando | O que faz | Como utilizar |
| ------- | --------- | ------------- |
| INSERT  |           |               |
| UPDATE  |           |               |
| DELETE  |           |               |

---
## Comandos DQL

| Comando  | O que faz | Como utilizar |
| -------- | --------- | ------------- |
| SELECT   |           |               |
| WHERE    |           |               |
| ORDER BY |           |               |

---
## Restrições de integridade

| Comando               | O que faz                                                                                                   | Como utilizar                                                  |
| --------------------- | ----------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------- |
| NOT NULL              | Não permite valores nulos                                                                                   | nome VARCHAR(10) NOT NULL                                      |
| PRIMARY KEY           | Define um atributo como chave primária                                                                      | PRIMARY KEY(Cpf)                                               |
| FOREIGN KEY           | Define um atributo como chave estrangeira                                                                   | FOREIGN KEY (Cpf_supervisor) REFERENCES Funcionario(Cpf)       |
| ON DELETE CASCADE     | Deleta os registros correspondentes nas tabelas referenciadas                                               | ON DELETE CASCADE                                              |
| ON UPDATE CASCADE     | Atualiza todos os registros referenciados por chaves estrangeiras                                           | ON UPDATE CASCADE                                              |
| ON DELETE SET NULL    | Ao removermos uma chave primária, as chaves estrangeiras virarão nulas                                      | ON DELETE SET NULL                                             |
| ON UPDATE SET NULL    | Ao modificarmos uma chave primária, as chaves estrangeiras virarão nulas                                    | ON UPDATE SET NULL                                             |
| ON DELETE SET DEFAULT | Ao removermos uma chave primária, um valor default será passado para as chaves estrangeiras referenciadas   | ON DELETE SET DEFAULT                                          |
| ON UPDATE SET NULL    | Ao modificarmos uma chave primária, um valor default seráp assado para as chaves estrangerias referenciadas | ON UPDATE SET DEFAULT                                          |
| CHECK                 | Define uma condição como restrição                                                                          | idade INT NOT NULL CHECK (idade>0)                             |
| UNIQUE                | Define uma chave alternativa                                                                                | nome VARCHAR(10) UNIQUE                                        |
| CONSTRAINT            | Define explicitamente um nome para uma restrição de integridade                                             | idade INT NOT NULL CONSTRAIN chk_idade_minima CHECK (idade>18) |

---
