<h1>Guia para desenvolvimento NodeJs com Typescript</h1>
<h5>(Em desenvolvimento!)</h5>
<br />
<br />
<br />

### Rodar comando abaixo para criar package.json:
```
yarn init -y
```
### Instalar express:
```
yarn add express

yarn add -D @types/express
```
### Instalar como devDependência o typescript:
```
yarn add -D typescript
```
### Rodar comando para gerar o arquivo de configuração "tsconfig.json" do typescript:
```
yarn tsc --init
```
### Criar pasta src com arquivo server.ts dentro.

### Abrir arquivo tsconfig.json e fazer as seguintes configurações:
```
"outDir": "./dist"
"rootDir": "./src"
```
<br />
<br />

**Obs: fazer reload do vscode para iniciar as configurações do arquivo tsconfig.json**
<br />

### Fazer configurações iniciais do server.ts

### Instalar modulo ts-node-dev:
```
yarn add -D ts-node-dev
```
### Configurar scripts no package.json para rodar servidor:
```
"scripts": {
  "build": "tsc",
  "dev:server": "ts-node-dev --inspect --ignore-watch node_modules src/server.ts"
},
```
### Criar pasta routes com os arquivos dentro:

clients.routes.ts
index.ts

### Voltar ao arquivo server.ts e deixa-lo com o seguinte código para incluir as rotas no arquivo principal:
```
import express from "express";

import routes from "./routes";

const app = express();

app.use(express.json());
app.use(routes);

app.listen(3333, () => {
  console.log("Server a runnning on port 3333");
});
```
### Fazer instalação dos pacotes typeorm e pg:

yarn add typeorm pg

### Criar pasta src/database contendo uma pasta migrations e um arquivo index.ts para configurar:

import { createConnection } from "typeorm";

createConnection();

### Criar arquivo ormconfig.json na raiz do projeto e configurar:

```
{
  "type": "postgres",
  "host": "localhost",
  "port": 5432,
  "username": "nome da conexão da base de dados",
  "password": "senha",
  "database": "nome do banco de dados"
}
```

### Dentro do arquivo ormconfig.json deixar a seguinte configuração para poder criar as migrations:

```
{
  "type": "postgres",
  "host": "localhost",
  "port": 5432,
  "username": "postgres",
  "password": "teste",
  "database": "bdteste",
  "entities": ["./src/models/*.ts"],
  "migrations": ["./src/database/migrations/*.ts"],
  "cli": {
    "migrationsDir": "./src/database/migrations"
  }
}
```
### Dentro do package.json incluir em scripts o comando:
```
"typeorm": "ts-node-dev ./node_modules/typeorm/cli.js"
```

### Rodar comando do typeorm para concluir configurações:
```
yarn typeorm
```

### Comando para criar uma migration:
```
yarn typeorm migration:create -n NomeDaMigrations
```

**Codificar a migration de acordo com o exemplo do projeto**


### Rodar comando para criar migration no banco de dados
```
yarn typeorm migration:run
```
