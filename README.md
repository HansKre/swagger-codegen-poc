# Swagger-Codegen-PoC

## Installation

[GitHub](https://github.com/swagger-api/swagger-codegen#compatibility)

```sh
brew install swagger-codegen
```

## Generate TypeScript Client

To generate a TS client for <https://petstore.swagger.io/v2/swagger.json>, please run the following:

```sh
# typescript-axios
# typescript-fetch
# mkdir -p api-client/ts
swagger-codegen generate -i https://petstore.swagger.io/v2/swagger.json \
    -l typescript-fetch \
    -o ./api-client/ts
```

## Setup Frontend

```sh
npm init vue@latest
# cd into project
# copy client into project
# install deps
npm install
# install isomorphic-fetch url
npm i isomorphic-fetch url
npm run format
npm run dev
```
