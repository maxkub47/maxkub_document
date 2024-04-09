---
id: 2
title: itoolkit
description: itoolkit is a Node.js interface to XMLSERVICE to access all things IBM i.
slug: /itoolkit
---

[Package Detail] https://www.npmjs.com/package/itoolkit <br/>
[Document] https://nodejs-itoolkit.readthedocs.io/en/latest

```powershell
npm install itoolkit
```

### Example Code

```jsx title="package.json"
{
  "name": "server",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "cors": "^2.8.5",
    "dotenv": "^16.0.1",
    "express": "^4.18.1",
    "itoolkit": "^1.0.0",
    "morgan": "^1.10.0",
    "nodemon": "^2.0.19"
  }
}
```

```jsx title="server.js"
const express = require("express");
const morgan = require("morgan");
const cors = require("cors");
require("dotenv").config();
const objdRoute = require("./route/objd");
const clcmdRoute = require("./route/clcmd");
const app = express();

//middleware
app.use(express.json());
app.use(cors());
app.use(morgan("dev"));

//route
app.use("/api", objdRoute);
app.use("/api", clcmdRoute);

const port = process.env.PORT || 8000;

app.listen(port, () => console.log(`Start Server in port ${port}`));
```

### Test Call CLP

```jsx title="route/clcmd.js"
const express = require("express");
const router = express.Router();
const { loaddata } = require("../controller/clcmdcontroller");

router.get("/sql", loaddata);

module.exports = router;
```

```jsx title="controller/clcmdcontroller.js"
exports.loaddata = (req, res) => {
  const { Connection, CommandCall } = require("itoolkit");
  const { parseString } = require("xml2js");

  const connection = new Connection({
    transport: "ssh",
    transportOptions: {
      host: process.env.HOST,
      username: process.env.USER,
      password: process.env.PASSWORD,
    },
  });

  const command = new CommandCall({
    type: "cl",
    //command: " RTVDTAARA DTAARA(MAXLIB/TESTDTA *ALL) RTNVAR(?)",
    //command:"CHGDTAARA DTAARA(MAXLIB/TESTDTA *ALL) VALUE('maxkub')"
    command: "ADDLIBLE LIB(MAXTOOL)",
    //command:"test"
  });

  connection.add(command);

  const command2 = new CommandCall({
    type: "cl",
    //command: " RTVDTAARA DTAARA(MAXLIB/TESTDTA *ALL) RTNVAR(?)",
    //command:"CHGDTAARA DTAARA(MAXLIB/TESTDTA *ALL) VALUE('maxkub')"
    command: "CALL PGM(MAXTOOL/TESTCALL)",
    //command:"test"
  });

  connection.add(command2);

  const command3 = new CommandCall({
    type: "cl",
    //command: " RTVDTAARA DTAARA(MAXLIB/TESTDTA *ALL) RTNVAR(?)",
    //command:"CHGDTAARA DTAARA(MAXLIB/TESTDTA *ALL) VALUE('maxkub')"
    command: "RTVDTAARA DTAARA(MAXtool/TSTDTA *ALL) RTNVAR(?)",
    //command:"test"
  });

  connection.add(command3);

  connection.run((error, xmlOutput) => {
    if (error) {
      throw error;
    }
    parseString(xmlOutput, (parseError, result) => {
      if (parseError) {
        throw parseError;
      }
      console.log(JSON.stringify(result));
      res.send(result);
    });
  });
};
```

### Test Call API

[API in AS400] https://www.ibm.com/docs/en/i/7.2?topic=interfaces-apis-by-category

```jsx title="route/objd.js"
const express = require("express");
const router = express.Router();
const { loaddata } = require("../controller/objdcontroller");

router.get("/objd", loaddata);

module.exports = router;
```

```jsx title="controller/objdcontroller.js"
exports.loaddata = (req, res) => {
  const { Connection, ProgramCall, xmlToJson } = require("itoolkit");
  const { parseString } = require("xml2js");

  const conn = new Connection({
    transport: "ssh",
    transportOptions: {
      host: process.env.HOST,
      username: process.env.USER,
      password: process.env.PASSWORD,
    },
  });

  const receiver = {
    name: "receiver",
    type: "ds",
    io: "out",
    len: "rec1",
    fields: [
      { name: "bytes_returned", type: "10i0", value: "0" },
      { name: "bytes_available", type: "10i0", value: "0" },
      { name: "object_name", type: "10A", value: "" },
      { name: "object_library_name", type: "10A", value: "" },
      { name: "object_type", type: "10A", value: "" },
      { name: "return_library", type: "10A", value: "0" },
      { name: "storage_pool_number", type: "10i0", value: "0" },
      { name: "object_owner", type: "10A", value: "" },
      { name: "object_domain", type: "2A", value: "" },
      { name: "creation_datetime", type: "13A", value: "" },
      { name: "object_change_datetime", type: "13A", value: "" },
      { name: "extended_object_attribute", type: "10A", value: "" },
      { name: "text_description", type: "50A", value: "" },
      { name: "source_file_name", type: "10A", value: "" },
      { name: "source_file_library_name", type: "10A", value: "" },
      { name: "source_file_member_name", type: "10A", value: "" },
    ],
  };

  const errno = {
    name: "error_code",
    type: "ds",
    io: "both",
    len: "rec2",
    fields: [
      {
        name: "bytes_provided",
        type: "10i0",
        value: 0,
        setlen: "rec2",
      },
      { name: "bytes_available", type: "10i0", value: 0 },
      { name: "msgid", type: "7A", value: "" },
      { type: "1A", value: "" },
    ],
  };

  const objectAndLibrary = {
    type: "ds",
    fields: [
      { name: "object", type: "10A", value: "TESTAPI" },
      { name: "lib", type: "10A", value: "MAXLIB" },
    ],
  };

  const program = new ProgramCall("QUSROBJD", { lib: "QSYS" });
  program.addParam(receiver);
  program.addParam({
    name: "length_of_receiver",
    type: "10i0",
    setlen: "rec1",
    value: "0",
  });
  program.addParam({ name: "format_name", type: "8A", value: "OBJD0200" });
  program.addParam(objectAndLibrary);
  program.addParam({ name: "object_type", type: "10A", value: "*PGM" });
  program.addParam(errno);

  conn.add(program);

  conn.run((error, xmlOutput) => {
    if (error) {
      throw error;
    }
    parseString(xmlOutput, (parseError, result) => {
      if (parseError) {
        throw parseError;
      }
      console.log(JSON.stringify(result));

      const result2 = xmlToJson(xmlOutput);
      console.log(result2);
      //res.send(xmlOutput)
      res.send(result2);

      //---- show data

      //-----
    });
  });
};
```
