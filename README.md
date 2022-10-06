


# Título do projeto

Um parágrafo de descrição do projeto vai aqui

## 🚀 Descrição do Projeto

Labenu Music Awards é um show anual de músicas organizado pela própria Labenu que conta com a participação de bandas super famosas nacionais e internacionais! Ele sempre acontece durante uma semana inteira, começando na manhã de segunda e encerrando na noite de domingo.

O LAMA (Labenu Music Awards) está previsto para acontecer no fim do ano e ainda não existe um back-end construído para gerenciar os eventos e ingressos do festival.

Para gerenciar o evento é necessário organizar e centralizar as informações dos shows em um servidor, que então disponibiliza os dados para o website no front-end (que já está criado). Além de controlar os eventos com suas bandas e datas do show, a aplicação também deve gerenciar os ingressos de cada show. A arena tem uma capacidade máxima de 5000 pessoas, portanto deve ser respeitado um limite máximo de ingressos por show.

## Entidades

## User (usuário)
* Representa os usuários de nossa aplicação. Todo usuário é composto pelas seguintes características:

id (string) e gerado pela própria aplicação

name (string)
<br>
email (string) único por usuário
<br>
password: senha hasheada (string)
<br>
role: enum "NORMAL" ou "ADMIN"
<br>
Show (show)
<br>

* Representa os shows da nossa aplicação. Cada show possui as seguintes características:

id (string) gerado pela própria aplicação
<br>
band (string) representando o nome da banda
<br>
startsAt (Date) representando a data da apresentação
<br>
tickets (number) representando os ingressos ainda disponíveis
<br>
Tabelas (MySQL)
<br>

* Lama_Users

id VARCHAR(255) e chave primária
<br>
name VARCHAR(255) e não-nulo
<br>
password VARCHAR(255) e não-nulo
<br>
role ENUM “NORMAL” ou “ADMIN” com padrão “NORMAL” não-nulo

* Lama_Shows

id VARCHAR(255) e chave primária
<br>
band VARCHAR(255) e não-nulo
<br>
starts_at: DATE e não-nulo
<br>
* Lama Tickets
<br>
id VARCHAR(255) e chave primária
<br>
show_id VARCHAR(255) e chave estrangeira referenciando a id de Labook_Shows
<br>
user_id VARCHAR(255) e chave estrangeira referenciando a id de Labook_Users

## 📋 Funcionalidades

Link para a documentação:
<br>
GetAllUsers

### 🔧 Setup

## Instruções

```
Instalando as dependências:
```
* npm install:
Instala todas as dependências listadas no package.json.
<br>

* Criando o arquivo .env:
<br>
Criar o arquivo .env e configurar com as informações de seu banco de dados.
<br>

PORT: 3003
<br>
DB_HOST = host
<br>
DB_USER = usuario
<br>
DB_PASSWORD = senha
<br>
DB_NAME = nome-do-banco-de-dados
<br>
JWT_KEY = "minha-senha-segura"
<br>
JWT_EXPIRES_IN = "24h"
<br>
BCRYPT_SALT_ROUNDS = 12

## Populando a tabela:
<br>
* npm run migrations:
Cria e popula as tabelas com dados mockados de usuários e shows.
Esse script deve ser executado apenas uma única vez
Se executado uma segunda vez, ele dropa as tabelas e reseta os dados mockados

## Executar o projeto:
* npm run dev:
Estabelece a conexão com o banco de dados e reinicia automaticamente o servidor localhost toda a vez que o projeto for alterado e salvo.

## 1. Cadastro de usuário

Método: POST
Caminho: /users/signup
Entrada: name, email, password
Saída: mensagem de cadastro de um novo usuário. Ao final, retorna um token de acesso ao sistema.
Validações e regras de negócio:
name, email e password devem ser fornecidos e serem do tipo string
name deve possuir ao menos 3 caracteres, enquanto password ao menos 6 caracteres
email deve ter um formato válido e único, não podendo repetir no banco de dado

## 2. Acesso de usuário
Método: POST
Caminho: /users/login
Entrada: email, password
Saída: mensagem de acesso de um usuário cadastrado no endpoint anterior. Ao final, retorna um token de acesso ao sistema.
Validações e regras de negócio:
email e password devem ser fornecidos e serem do tipo string
password deve possuir ao menos 6 caracteres
email deve ter um formato válido
O usuário com o email fornecido deve existir no sistema

## 3. Cria um novo show (protegido)

Método POST
Caminho /shows
Entrada token de acesso, band, startsAt
Saída: mensagem de show criado com sucesso e os dados do show em si
Validações e regras de negócio:
a data do show não pode ser anterior ao início do festival (5 de dezembro)
só pode existir um show por dia durante o evento
Observação: este endpoint deve ser acessível apenas aos admins.

## 4. Buscar shows
Método: GET
Caminho: /shows
Entrada: nenhuma
Saída uma lista com todos os shows agendados
Validações e regras de negócio:
dentre as informações dos shows, deve existir também o número de ingressos disponíveis (iniciando em 5000)

## 5. Criação da reserva de ingresso (protegido)
Método: POST
Caminho: /shows/:id
Entrada: token de acesso, id do show a ser reservado
Saída: mensagem de reserva realizada com sucesso
Validações e regras de negócio:
id do show reservado deve existir no banco de dados
uma mesma pessoa só pode reservar um ingresso para cada show
deve ser respeitado o limite de 5000 ingressos por show
Observação: este endpoint deve ser acessível apenas aos admins.

## 6. Remoção da reserva de ingresso (protegido)
Método: DELETE
Caminho:/shows/:id
Entrada: token de acesso, id do show a ser removido
Saída: mensagem de reserva removida com sucesso
Validações e regras de negócio:
id do show reservado deve existir no banco de dados
a pessoa já deve ter reservado o ingresso
Observação: este endpoint deve ser acessível apenas aos admins.

## Referências
Projeto Cookenu Backend
<br>
Projeto LabE-commerce Backend
<br>
Projeto Labook
<br>
Katherine Peterson

## Documentação (links):
Heroku
<br>
Postman


## 🛠️ Tecnologias Utilizadas

Mencione as ferramentas que você usou para criar seu projeto

* [Typescript](https://www.typescriptlang.org/docs/)
* [Express](https://expressjs.com/)
* [Knex](https://knexjs.org/)
* [MySQL](https://www.mysql.com/)

## ✒️ Autores

## INTEGRANTE
Perfil      | Link do perfil no GITHUB
--------- | ------
[<img src="https://media-exp1.licdn.com/dms/image/C4D03AQGF3EBuZED7DA/profile-displayphoto-shrink_800_800/0/1660667280345?e=1670457600&v=beta&t=irvfDUXElwXnTMD00dSdmYek-dVhEPzgs0foKTri62E" width="75px;"/>](https://github.com/Lakshmi-Monteiro-Bittencourt) | [Laksmin Monteiro Bittencourt]

