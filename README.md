<h1 align="center">Welcome to react-docker👋</h1>
<p>
  <img src="https://img.shields.io/badge/node-%3E%3D14-blue.svg" />
  <img src="https://img.shields.io/badge/docker-%3E%3D20.10.9-blue.svg" />
  <a href="https://www.npmjs.com/package/react-demo" target="_blank">
    <img alt="Version" src="https://img.shields.io/npm/v/react-demo.svg">
  </a>
  <a href="#" target="_blank">
    <img alt="License: MIT" src="https://img.shields.io/badge/License-MIT-yellow.svg" />
  </a>
</p>

> Projeto para o desafio de DevOps utilizando React, Docker e NGINX

## Prerequisites

- node >=14
- docker >= 20.10.9

* Caso não tenha o docker intalado entre no link (https://docs.docker.com/engine/install)

O projeto contem dois containers, um no modo desenvolvimento e outro para o modo de produção

## Dockerfile.dev
A configuração do modo desenvolvimento está no arquivo Dockerfile.dev

```
FROM node

WORKDIR /app

COPY package.json .

RUN  yarn install

COPY . .

ARG REACT_APP_NAME

ENV REACT_APP_NAME=Mizael-dev

EXPOSE 3000

CMD ["yarn", "start"]
```

## Dockerfile.prod
A configuração do modo de produção está no arquivo Dockerfile.prod com a configuração do NGINX

```
FROM node as build

WORKDIR /app

COPY package.json .

RUN  yarn install

COPY . .

ARG REACT_APP_NAME

ENV REACT_APP_NAME=$REACT_APP_NAME

EXPOSE 3000

RUN npm run build


FROM nginx

COPY --from=build /app/build /usr/share/nginx/html
```


## Criar a imagem e iniciar o container no modo desenvolvimento
```sh
docker-compose -f docker-compose.yml -f docker-compose-dev.yml up -d --build
```
> Servidor de desenvolvimento abre na porta (http://localhost:4000) 

## Criar a imagem e iniciar o container no modo produção
```sh
docker-compose -f docker-compose.yml -f docker-compose-prod.yml up -d --build
```
> Servidor de produção abre na porta (http://localhost:8080) 

## Author

👤 **Mizael Alves**

* Github: [@mizaelalves](https://github.com/mizaelalves)
* LinkedIn: [@mizaelalves](https://linkedin.com/in/mizaelalves)

> SO utilizado ZorinOS 16

## Show your support

Give a ⭐️ if this project helped you!

***
_This README was generated with ❤️ by [readme-md-generator](https://github.com/kefranabg/readme-md-generator)_
