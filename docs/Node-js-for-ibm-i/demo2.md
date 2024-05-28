---
sidebar_position: 5
title: Demo for Aeon
---
## nodeJS

```javascript title="package.json"
{
  "name": "demo_node_aeon",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "cors": "^2.8.5",
    "express": "^4.19.2",
    "morgan": "^1.10.0",
    "odbc": "^2.4.8"
  }
}

```

```javascript title="Server.js"
const express = require("express");
const morgan = require("morgan");
const cors = require("cors");
const app = express();
const odbc = require("odbc");

const port = 9110;

//middleware
app.use(express.json());
app.use(cors());
app.use(morgan("dev"));

app.get("/", (req, res) => {
  res.send("Welcome to My NodeJS");
});

app.get("/odbc", async (req, res) => {
  const connection = await odbc.pool(
    [
      `DRIVER=IBM i Access ODBC Driver`,
      `SYSTEM=172.16.1.240`,
      `UID=TSTODBC`,
      `Password=TSTODBC`,
      `Naming=1`,
      `DBQ=MAXLIB1`,
    ].join(";")
  );
  results = await connection.query("select * from MAXLIB1.FILE1");
  res.send(results);
});

app.listen(port, () => console.log(`Run Server in port ${port}`));

```


## React

```
npm create vite@latest demo_aeon -- --template react
cd demo_aeon
npm i

npm run dev
mkdir demo_aeon
scp -r * max@172.16.1.240:/www/apachedft/htdocs/demo_aeon
```

```javascript title="vite.config.js"
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [react()],
  //for prod.
  base: "/demo_aeon/",
  //for dev.
  //base: '/',
  build: {
    outDir: 'dist',
    sourcemap: true,
    emptyOutDir: true,
    rollupOptions: {
      entrtFileNames: '[name].js',
      chunkFileNames: '[name].js',
      assetFileNames: '[name].[ext]',
    },
  },
})
```

