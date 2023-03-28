# Swagger-Codegen-PoC

[Documentation](https://github.com/swagger-api/swagger-codegen#compatibility)

## Installation OSX

```sh
brew install swagger-codegen
```

## Generate TypeScript Client OSX

To generate a TS client for <https://petstore.swagger.io/v2/swagger.json>, please run the following:

```sh
# supported typescript clients: typescript-axios, typescript-fetch
# mkdir -p api-client/ts
swagger-codegen generate -i https://petstore.swagger.io/v2/swagger.json \
    -l typescript-fetch \
    -o ./api-client/ts
```

## Installation Windows

```powershell
# download
wget https://repo1.maven.org/maven2/io/swagger/codegen/v3/swagger-codegen-cli/3.0.41/swagger-codegen-cli-3.0.41.jar -O swagger-codegen-cli.jar

# test
java -jar swagger-codegen-cli.jar --help
```

### Generate TypeScript Client on Windows (from local `swagger.json`)

```powershell
# download swagger-json
wget https://petstore.swagger.io/v2/swagger.json -O swagger.json
# create folder
mkdir api-client
# supported typescript clients: typescript-axios, typescript-fetch
java -jar swagger-codegen-cli.jar generate -i swagger.json -l typescript-fetch -o ./api-client
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

## Remove unused components

```sh
# remove unused components
# https://github.com/Redocly/redocly-cli
npm install @redocly/cli -g
redocly bundle --remove-unused-components .\swagger-removed-paths.json -o .\swagger-no-unused.json
# repeat until no components were removed
redocly bundle --remove-unused-components .\swagger-no-unused.json -o .\swagger-no-unused.json
# verify
redocly lint .\swagger-no-unused.json
```
