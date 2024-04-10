---
id: 1
title: ODBC for IBM i
description: An asynchronous interface for Node.js to unixODBC and its supported drivers.
slug: /node-js/odbc-for-i
---

[Package Detail] https://www.npmjs.com/package/odbc

```jsx
npm install odbc
```

### Example code

```jsx title="package.json"
{
  "dependencies": {
    "cor": "^0.0.0",
    "cors": "^2.8.5",
    "dotenv": "^16.0.1",
    "express": "^4.18.1",
    "morgan": "^1.10.0",
    "nodemon": "^2.0.19",
    "odbc": "^2.4.4"
  },
  "name": "server",
  "version": "1.0.0",
  "main": "app.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "run": "nodemon app.js"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "description": ""
}
```

```jsx title="server.js"
const express = require("express");
const morgan = require("morgan");
const cors = require("cors");
require("dotenv").config();
const userRoute = require("./route/user");
const app = express();

//middleware
app.use(express.json());
app.use(cors());
app.use(morgan("dev"));

//route
app.use("/api", userRoute);

const port = process.env.PORT || 8000;

app.listen(port, () => console.log(`Start Server in port ${port}`));
```

```jsx title="route/route.js"
const express = require("express");
const router = express.Router();
const { loaddata } = require("../controller/usercontroller");

router.get("/user", loaddata);

module.exports = router;
```

```jsx title="controller/controller.js"
const connection = require("../server");
const odbc = require("odbc");

exports.loaddata = (req, res) => {
  //connect Database
  const cn = "DSN=maxsysDSN;UID=max;PWD=maxkub";
  odbc.connect(cn, (err, connection) => {
    connection.query(
      "SELECT * FROM prd1dblib.fi005p FETCH FIRST 6 ROWS ONLY",
      (error, result) => {
        if (error) {
          throw error;
        }
        console.log(result);
        res.json(result);
      }
    );
  });
};
```
