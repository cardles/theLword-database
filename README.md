# {reprograma} week 12: database search challenge
Desafio apresentado ao curso online de back-end da {reprograma}. <br>
Tema da semana: *"Banco de Dados: Introdução ao MongoDB"*.

## iniciando o MongoDB
Para iniciar o desafio, foi necessário rodar o servidor, iniciar o MongoDB e abrir o o programa Robo 3T. <br>

- Passo-a-passo:
* `/c/Program Files/MongoDB/Server/5.0/bin` é o caminho no qual o terminal precisa estar para executar os comandos:

    * `./mongod` roda o servidor do banco de dados no terminal *bash*.
    * `./mongo` inicia o Mongo no computador pelo terminal *bash*.

* Após realizar esse processo, é necessário abrir o programa Robo 3T e criar uma *connection*, especificando o endereço e a porta que correspondem ao local onde está rodando o MongoDB. <br>
* Dentro da *connection* é necessário criar um *database* e, dentro dele, uma *collection*. <br>
Pronto, já temos o necessário para começar!

## dados utilizados
Os dados que foram utilizados no bando de dados estão disponíveis dentro da pasta *data*, na qual consta o arquivo `characters-TLW.json`, criado por mim e baseado na série **The L Word**, da *Showtime*.


## seletores utilizados
Os seletores abaixo foram utilizados no Robo 3T, conectado ao banco de dados MongoDB: <br>


- Inserir vários *documents* simultaneamente
Em uma *New Set*, insere arquivo .json completo, criando *documents* automaticamente dentro da *collection*

    * `insertMany()` permite que vários objetos sejam inseridos ao mesmo tempo, gerando *documents* separados.

`db.getCollection('characters-TLW').insertMany( *characters-TLW.json* )`


- Atualizar *document*
Inclui um novo atributo em um *document* existente, encontrando-o através do atributo declarado.

    * `{$set: { } }` permite que todo o conteúdo adicionado dentro de {} não substitua os outros atributos do *document*, apenas adicione novos.


`db.getCollection('characters-TLW').update({ " name" : "Bette Porter" }, {$set: { "iLove": true }})`

`db.getCollection('characters-TLW').update({ "name" : "Shane McCutcheon" }, {$set: { "iLove": false }})`

`db.getCollection('characters-TLW').update({ "name" : "Alice Pieszecki"}, {$set: { "iLove": false }})`

`db.getCollection('characters-TLW').update({ "name" : "Dani Núñez" }, {$set: { "iLove": true }})`

`db.getCollection('characters-TLW').update({ "name" : "Sarah Finley" }, {$set: { "iLove": true }})`

`db.getCollection('characters-TLW').update({ "name" : "Tina Kennard" }, {$set: { "iLove": true }})`

`db.getCollection('characters-TLW').update({ "name" : "Helena Peabody" }, {$set: { "iLove": false }})`

`db.getCollection('characters-TLW').update({ "name" : "Jenny Schecter" }, {$set: { "iLove": false }})`


- Remover *document*
Remove o *document* por completo, encontrando-o através do atributo declarado. <br>

Para remover o *document* que recebe `Jenny Schecter` como valor da chave `name`:
`db.getCollection('characters-TLW').remove({ "name" : "Jenny Schecter" })`


- Pesquisar com projeção
Oculta ou apresenta atributos dentro dos *documents*. <br>

Para apresentar apenas os atributos `name` e `iLove`:
`db.getCollection('characters-TLW').find({}, { "name": 1, "iLove": 1 })`

Para não apresentar apenas o atributo `presentIn`:
`db.getCollection('characters-TLW').find({}, {"presentIn": 0})`


- Pesquisar utilizando combinação entre os seletores
    * `find{}` é responsável pela visualização dos *documents*. Ao definir um atributo, apenas os itens que corresponderem a ele serão apresentados na tela.
    * `{ key: value }` não apresenta (value = 0) ou apresenta (value = 1) o atributo que contiver a chave declarada.

`db.getCollection('characters-TLW').find({"iLove": true}, {"about": 0})`


- Pesquisar de forma paginada e ordenada
    * `sort{ chave: 1 }` ordena os *documents* por ordem crescente (value = 1) ou decrescente (value = -1) a partir da chave declarada.
    * `limit( value )` limita a apresentação de *documents* à quantidade inserida em *value*.
    * `skip( value )` pula, do ultimo para o primeiro, a quantidade de *documents* inserida em *value*.

`db.getCollection('characters-TLW').find().sort({ "name": 1 }).skip( 4 ).limit( 3 )`


- Pesquisar com array
Encontra *document* por uma lista, sendo necessário declarar a chave da lista e o atributo do objeto.

    * `$elemMatch` percorre os atributos (elements) dentro da lista `presentIn` e checa se um corresponde ao outro, retornando *documents* que contenham o atributo declarado.

`db.getCollection('characters-TLW').find({ "presentIn": {$elemMatch: { "originalVersion": "Mia Kirshner, Jennifer Beals, Pam Grier, Laurel Holloman, Erin Daniels, Leisha Hailey and Katherine Moennig star in this intimate drama series about a group of lesbian friends struggling with romance and careers in Los Angeles" }}})`


## bibliografia
https://thelwordguide.weebly.com/character-guide.html
https://the-l-word.fandom.com/wiki/The_L_Word_wiki