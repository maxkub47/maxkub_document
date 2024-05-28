---
sidebar_position: 5
title: Demo for Aeon
---

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

const port = 9000;

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
