# Koa2 starter REST API application

## Technologies:

- Koa v2
- ES 7
- MySQL
- REST API
- JWT Tokens
- JSON Schema
- Yarn
- ESLint
- Git hooks

## Description:
This Koa 2 REST API boilerplate based on fork from awesome <a href="https://github.com/S-PRO/koa2-starter">Alexander Kazantsev node.js/koa boilerplate</a><br>
Features:
<ul>
<li>MVC like Pattern</li>
<li>REST API</li>
<li>Built in Email/password Authorization using JWT tokens</li>
<li>Built in File upload methods</li>
<li>Public and Auth protected routes</li>
</ul>

## Getting started

Create data base:

    CREATE DATABASE `koa2-starter` CHARACTER SET utf8 COLLATE utf8_general_ci;

Install Sequelize CLI:

    $ npm i -g sequelize-cli

Install dependencies:

    $ yarn install

Make migrations and seeds:

    $ sequelize db:migrate
    $ sequelize db:seed:all

Run locally:

    $ npm start

## Project structure

```
.
└── app/  --> Application files
    ├── config/
    |   ├── app.confg.js    --> App config: port, base url, etc...
        ├── database.json   --> databes configuration file generated by sequelize cli
    |   └── token.confg.js  --> App JWT Token config
    ├── controllers/        --> All custom controllers should be stored in this folder
    ├── methods/            --> All custom methods for buisness logic should be stored in this folder
    ├── db/
    |   └── migrations/             --> Migrations generated by sequelize cli
    |       ├── 20170122100838-create-user.js    
    |       schemas/
    |       ├── index.js            --> Collect all schemas  
    |       └── create.schema.json  --> JSON Schema
    |       seeders/                --> Seeds generated sequelize cli
    |       ├── 20170122102315-users.js
    |       models/                 --> Models generated sequelize cli
    |       ├── 20170122102315-users.js
    ├── middlewares/          --> All custom middlewares should be stored in this folder
    ├── router/
    |   ├── index.js          --> Export routes
    |   ├── private.routes.js --> Private routes
    |   └── public.routes.js  --> Public routes
    ├── utils/                --> Application common utils
    └── index.js              --> Application entry point
└── upload/                   --> Application uploaded files folder
```

## REST API Endpoint examples

Public

    $ http POST localhost:3000/auth/signin password=foo email=bar@gmail.com

    ```json
    {
      "accessToken": "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MiwiZmlyc3RfbmFtZSI6ImRvZnRyZXFlZXEiLCJsYXN0X25hbWUiOiJqb3JmdGhxbmVlcSIsImVtYWlsIjoiZG9lZXFyZnRlcUBlbWFpbC5jb20iLCJwYXNzd29yZCI6IiQ2JDFhY2VjMmY5JDQxNDgxNjU2NmZkYWM3ZGQ2ZjRlNTMyZmEwNTZiZDQxODQ0ZTkyYjU1Yzc3MWI1NmEwY2FlZTMzNmY2MWRmOWI3OGU2YWRlNWVhOWE2N2EzMTM3MDFkZmFhOWYwNjQzN2Q5YmViNTFhYzU0YTk5MTVjYWJmMjI2MmNhOWFkY2Q0Iiwic3RhdHVzIjoiYWN0aXZlIiwiaWF0IjoxNDkxODE1OTMzLCJleHAiOjE1MjMzNzM1MzN9._noWQAdCc0w4TWIvBisR7qUWgn7iN7ffGL6e67wB_wY",
      "refreshToken": "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MiwiZmlyc3RfbmFtZSI6ImRvZnRyZXFlZXEiLCJsYXN0X25hbWUiOiJqb3JmdGhxbmVlcSIsImVtYWlsIjoiZG9lZXFyZnRlcUBlbWFpbC5jb20iLCJwYXNzd29yZCI6IiQ2JDFhY2VjMmY5JDQxNDgxNjU2NmZkYWM3ZGQ2ZjRlNTMyZmEwNTZiZDQxODQ0ZTkyYjU1Yzc3MWI1NmEwY2FlZTMzNmY2MWRmOWI3OGU2YWRlNWVhOWE2N2EzMTM3MDFkZmFhOWYwNjQzN2Q5YmViNTFhYzU0YTk5MTVjYWJmMjI2MmNhOWFkY2Q0Iiwic3RhdHVzIjoiYWN0aXZlIiwiaWF0IjoxNDkxODE1OTMzLCJleHAiOjE1MjMzNzM1MzN9._noWQAdCc0w4TWIvBisR7qUWgn7iN7ffGL6e67wB_wY"
    }
    ```

    $ http POST localhost:3000/auth/signup first_name=john last_name=doe password=foo email=bar

    ```json
    {
      "accessToken": "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJmaXJzdF9uYW1lIjoiZDZob2pnZ2J0N2dmdHJlcWU5ZXEiLCJsYXN0X25hbWUiOiJqb3JoNmdqZ2J0Z2Z0N2hxbmVoOWVxIiwiZW1haWwiOiJkb2U2Z2doamVxcmd0ZmJ0N2VxQGVtOWFpbC5jb20iLCJwYXNzd29yZCI6IiQ2JDQxZTAxNGVkJDhiOWJiNzU0YWYzZWY3ZWNlZGM0OGIzZjJiZTY3ZjYyZjQ1NmY4NjFmYmY0ZmJiNDU1ZWNlY2UyOWMzNmJhNTU5NjJiYWRhYTgyNjQ4NzE1ZjRmOTFkMTc4MDg1MTJlYjk2MGY2NzZmOGE5MDA3OGFiZDBjNWJmMWIyMWZkYjE5IiwiaWF0IjoxNDkxODE2MDkzLCJleHAiOjE1MjMzNzM2OTN9.E5D9JAJw5HZyt-GcZNS89S4qqC5Md5aHuntcxEDsI3M",
      "refreshToken": "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJmaXJzdF9uYW1lIjoiZDZob2pnZ2J0N2dmdHJlcWU5ZXEiLCJsYXN0X25hbWUiOiJqb3JoNmdqZ2J0Z2Z0N2hxbmVoOWVxIiwiZW1haWwiOiJkb2U2Z2doamVxcmd0ZmJ0N2VxQGVtOWFpbC5jb20iLCJwYXNzd29yZCI6IiQ2JDQxZTAxNGVkJDhiOWJiNzU0YWYzZWY3ZWNlZGM0OGIzZjJiZTY3ZjYyZjQ1NmY4NjFmYmY0ZmJiNDU1ZWNlY2UyOWMzNmJhNTU5NjJiYWRhYTgyNjQ4NzE1ZjRmOTFkMTc4MDg1MTJlYjk2MGY2NzZmOGE5MDA3OGFiZDBjNWJmMWIyMWZkYjE5IiwiaWF0IjoxNDkxODE2MDkzLCJleHAiOjE1MjMzNzM2OTN9.E5D9JAJw5HZyt-GcZNS89S4qqC5Md5aHuntcxEDsI3M"
    }
    ```

    $ http POST localhost:3000/auth/refreshtoken refreshToken=Bearer Token

    ```json
    {
      "accessToken": "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MiwiZmlyc3RfbmFtZSI6ImRvZnRyZXFlZXEiLCJsYXN0X25hbWUiOiJqb3JmdGhxbmVlcSIsImVtYWlsIjoiZG9lZXFyZnRlcUBlbWFpbC5jb20iLCJwYXNzd29yZCI6IiQ2JDFhY2VjMmY5JDQxNDgxNjU2NmZkYWM3ZGQ2ZjRlNTMyZmEwNTZiZDQxODQ0ZTkyYjU1Yzc3MWI1NmEwY2FlZTMzNmY2MWRmOWI3OGU2YWRlNWVhOWE2N2EzMTM3MDFkZmFhOWYwNjQzN2Q5YmViNTFhYzU0YTk5MTVjYWJmMjI2MmNhOWFkY2Q0Iiwic3RhdHVzIjoiYWN0aXZlIiwiaWF0IjoxNDkxODE2MjQwLCJleHAiOjE1MjMzNzM4NDB9.EQCQOkMVb9afM6t-iH5YWDdiGBGrwobdOwOVITP2AgA",
      "refreshToken": "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MiwiZmlyc3RfbmFtZSI6ImRvZnRyZXFlZXEiLCJsYXN0X25hbWUiOiJqb3JmdGhxbmVlcSIsImVtYWlsIjoiZG9lZXFyZnRlcUBlbWFpbC5jb20iLCJwYXNzd29yZCI6IiQ2JDFhY2VjMmY5JDQxNDgxNjU2NmZkYWM3ZGQ2ZjRlNTMyZmEwNTZiZDQxODQ0ZTkyYjU1Yzc3MWI1NmEwY2FlZTMzNmY2MWRmOWI3OGU2YWRlNWVhOWE2N2EzMTM3MDFkZmFhOWYwNjQzN2Q5YmViNTFhYzU0YTk5MTVjYWJmMjI2MmNhOWFkY2Q0Iiwic3RhdHVzIjoiYWN0aXZlIiwiaWF0IjoxNDkxODE2MjQwLCJleHAiOjE1MjMzNzM4NDB9.EQCQOkMVb9afM6t-iH5YWDdiGBGrwobdOwOVITP2AgA"
    }
    ```

    $ http POST localhost:3000/file/upload  file=file
    ```json
    {
        "upload":"true"
    }
    ```
    $ http DELETE localhost:3000/file/delete path=file.jpg
    ```json
    {
        "delete":"true"
    }
    ```
    $ http GET localhost:3000/file/exist/file.jpg
    ```json
    {
        "exist":"true"
    }
    ```
    $ http GET localhost:3000/file/fullpath/file.jpg
    ```json
    {
        "path":"/home/koa2-starter/uploads/53d3c059-03fd-4b71-9da4-821e0c31dd0f.png"
    }
    ```
    $ http GET localhost:3000/public/route

    ```json
    {
        "text":"public route"
    }
    ```

Private

HEADERS:
- Authorization:Bearer Token

    $ http GET localhost:3000/private/route

    ```json
    {
        "text":"private route"
    }
    ```

    $ http POST localhost:3000/auth/getuser

    ```json
    {
      "users": [
        {
          "createdAt": "2017-01-22T14:21:46.000Z",
          "email": "foo@bar.com",
          "first_name": "foo",
          "id": 4,
          "last_name": "bar",
          "status": "active",
          "updatedAt": "2017-01-22T14:21:46.000Z"
        }
      ]
    }
    ```

    $ http GET localhost:3000/user

```json
{
  "users": [
    {
      "createdAt": "2017-01-22T14:21:46.000Z",
      "email": "foo@bar.com",
      "first_name": "foo",
      "id": 4,
      "last_name": "bar",
      "status": "active",
      "updatedAt": "2017-01-22T14:21:46.000Z"
    }
  ]
}
```

    $ http GET localhost:3000/user/:id

```json
{
  "user": {
    "createdAt": "2017-01-22T14:21:46.000Z",
    "email": "foo@bar.com",
    "first_name": "foo",
    "id": 4,
    "last_name": "bar",
    "status": "active",
    "updatedAt": "2017-01-22T14:21:46.000Z"
  }
}
```

    $ http POST localhost:3000/user first_name=foo last_name=bar password=qwerty email=foo@bar.com

```json
{
  "user": {
    "createdAt": "2017-01-22T14:21:46.000Z",
    "email": "foo@bar.com",
    "first_name": "foo",
    "id": 4,
    "last_name": "bar",
    "status": "active",
    "updatedAt": "2017-01-22T14:21:46.000Z"
  }
}
```

    $ http PUT localhost:3000/user first_name=another_name last_name=bar email=foo@bar.com

```json
{
  "user": {
    "createdAt": "2017-01-22T14:21:46.000Z",
    "email": "foo@bar.com",
    "first_name": "another_name",
    "id": 4,
    "last_name": "bar",
    "status": "active",
    "updatedAt": "2017-01-22T14:21:46.000Z"
  }
}
```

    $ http DELETE localhost:3000/user/:id

```json
"204 No Content"
```



## TODO

- [ ] Add unit tests
- [ ] Add production deployment system
- [ ] Add ACLs
