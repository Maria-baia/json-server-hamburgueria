<h1 align="center">
  Atividade - JSON-Server do início ao Deploy
</h1>

<p align = "center">
Esta é uma Fake-API hospedada no Heroku onde é possível realizar requisições seguindo os parâmetros abaixo.
</p>

<p align="center">
  <a href="#endpoints">Endpoints</a>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</p>


## **Endpoints**

A API tem um total de 3 endpoints, sendo em volta principalmente do usuário - podendo cadastrar seu perfil, fazer login, colocar itens em seu carrinho, acessar carrinho e ver produtos. <br/>
O JSON para utilizar no Insomnia é este aqui -> https://git.heroku.com/json-server-hamburgueria2.git

Para importar o JSON no Insomnia é só clicar na palavra "Insomnia" no canto superior esquerdo. Nesse dropdown é só clicar em "Import / Export > Import Data > From Url" e colocar o link acima :v:

<!-- O url base da API é https://atividade-json.herokuapp.com/ -->

## Rotas que não precisam de autenticação

<h2 align ='center'> Criação de usuário </h2>

`POST /register -  FORMATO DA REQUISIÇÃO`
```json
{
  "name": "Maria",
  "email": "maria@gmail.com",
  "password": "123456",
}
```

Caso dê tudo certo, a resposta será assim:

`POST /register -  FORMATO DA RESPOSTA - STATUS 201`
```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6Im1hcmlhQGdtYWlsLmNvbSIsImlhdCI6MTYzNTgwMTkzMywiZXhwIjoxNjM1ODA1NTMzLCJzdWIiOiIxIn0.5CXPhST0j01EWv-JVBqAtcXHgtoiaMXWfgab6vBuAbc",
  "user": {
    "email": "maria@gmail.com",
    "name": "Maria",
    "id": 1
  }
}
```

<h2 align ='center'> Possíveis erros </h2>
```

Email já cadastrado:

`POST /register - `
``  FORMATO DA RESPOSTA - STATUS 400``
```json

 "Email already exists"

```

<h2 align = "center"> Login </h2>

`POST /login - FORMATO DA REQUISIÇÃO`
```json
{
  "email": "maria@gmail.com",
  "password": "123456"
}
```

Caso dê tudo certo, a resposta será assim:

`POST /login -  FORMATO DA RESPOSTA - STATUS 201`
```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6Im1hcmlhQGdtYWlsLmNvbSIsImlhdCI6MTYzNTg4NTIxOCwiZXhwIjoxNjM1ODg4ODE4LCJzdWIiOiIxIn0.inGbKEj3fhVraM1E9pXmk-c_uP1IYpQTWd9B-3M29XU",
  "user": {
    "email": "maria@gmail.com",
    "name": "Maria",
    "id": 1
  }
}
```

Com essa resposta, vemos que temos duas informações, o user e o token respectivo, dessa forma você pode guardar o token e o usuário logado no localStorage para fazer a gestão do usuário no seu frontend.

<h2 align ='center'> Listando carrinho. </h2>

`GET /carrinho?userId=:id -  FORMATO DA REQUISIÇÃO`
```json
[
  {
    "id": 1,
    "name": "Hamburguer",
    "category": "Sanduíches",
    "price": 14,
    "img": "../Assets/hamburguer",
    "userId": 1
  }
]

```

## Rotas que necessitam de autorização

Rotas que necessitam de autorização deve ser informado no cabeçalho da requisição o campo "Authorization", dessa forma:

> Authorization: Bearer {token}

<h2 align ='center'> Adição de item ao carrinho. </h2>

`POST /cart -  FORMATO DA REQUISIÇÃO`
```json
[
  {
      "name": "Hamburguer",
      "category": "Sanduíches",
      "price": 14,
      "img": "../Assets/hamburguer",
			"userId": 1
  }
]

```

Após o usuário estar logado, ele deve conseguir ler suas informações.

<h2 align ='center'> Listando informações do usuário. </h2>

Nessa aplicação o usuário precisa fazer login ou se cadastrar para ver suas informações já cadastradas na plataforma, na API podemos acessar dessa forma:
Aqui conseguimos ver o email, sua senha criptografada, nome, idade e id de usuário.

`GET /users/:id -  FORMATO DA RESPOSTA - STATUS 200`
```json
{
  "email": "maria@gmail.com",
  "password": "$2a$10$hyF1lVktAscW42K1vljCO.5RReMxTUGXF5bGLMd9uA2rXQzBHlP.e",
  "name": "Maria",
  "id": 1
}

```

<h2 align ='center'> Ver os produtos. </h2>

`GET /foods -  FORMATO DA RESPOSTA - STATUS 200`
```json
[
  {
    "id": 1,
    "name": "Hamburguer",
    "category": "Sanduíches",
    "price": 14,
    "img": "../Assets/hamburguer"
  },
  {
    "id": 2,
    "name": "X-Burguer",
    "category": "Sanduíches",
    "price": 16,
    "img": "../Assets/xburguer"
  },
  {
    "id": 3,
    "name": "Big Kenzie",
    "category": "Sanduíches",
    "price": 18,
    "img": "../Assets/bigKenzie"
  },
  {
    "id": 4,
    "name": "Combo Kenzie",
    "category": "Combos",
    "price": 26,
    "img": "../Assets/comboKenzie"
  },
  {
    "id": 5,
    "name": "Fanta Guaraná",
    "category": "Bebidas",
    "price": 5,
    "img": "../Assets/fantaGuarana"
  },
  {
    "id": 6,
    "name": "Coca Cola",
    "category": "Bebidas",
    "price": 7,
    "img": "../Assets/cocaCola"
  },
  {
    "id": 7,
    "name": "McShake Ovomaltine",
    "category": "Sobremesas",
    "price": 10,
    "img": "../Assets/mcShakeOvomaltine"
  },
  {
    "id": 8,
    "name": "Sundae Ovomaltine",
    "category": "Sobremesas",
    "price": 10,
    "img": "../Assets/sundaeOvomaltine"
  }
]

```

<h2 align ='center'> Apagar item do carrinho. </h2>

`DELETE /cart/:id - FORMATO DA RESPOSTA - STATUS 200`
```json
{}
```

---
Feito com ♥ by maria-baia :wave:
