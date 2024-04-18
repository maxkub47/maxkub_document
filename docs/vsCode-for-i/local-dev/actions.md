---
title: Local Actions
sidebar:
    order: 4 
---



Similar to other repository settings, users can now store Actions as part of the Workspace. Users can now create `.vscode/actions.json` inside of your Workspace, and can contain Actions that are specific to that Workspace. That configuration file should also be checked into git for that application.

Running local Actions will execute the commands with the working directory as the deploy directory.

There is a tool that can generate an initial `actions.json` file for you. After connecting to a system, open the command palette (F1) and search for 'Launch Actions Setup'. This shows a multi-select window where the user can pick which technologies they're using. Based on the selection, an `actions.json` will be created.

## Available variables

These variables can be used for local development. They can be referenced in `actions.json` or `.env`.

### Libraries

| Variable        | Description                                                                       |
| --------------- | --------------------------------------------------------------------------------- |
| `&BUILDLIB`     | The same as `&CURLIB`                                                             |
| `&CURLIB`       | The current library defined in the User Library List view. Can also use `*CURLIB` |
| `&LIBLS`        | The library list with spaces between each item                                    |
| `&BRANCHLIB`    | A deterministic library name built from the current branch in git                 |

### Directories and Files

| Variable        | Description                                                                       |
| --------------- | --------------------------------------------------------------------------------- |
| `&RELATIVEPATH` | The relative path to the file in the workspace                                    |
| `&LOCALPATH`    | The full path to the file on the local machine                                    |
| `&FULLPATH`     | The full path to the file on the remote machine                                   |
| `&WORKDIR`      | The working directory. Typically this means the deploy directory                  |
| `&FILEDIR`      | The directory of the file on the remote machine                                   |
| `&PARENT`       | The local parent directory                                                        |
| `&BASENAME`     | The basename of the file (`name.ext`). Can also use `{filename}`                  |
| `&NAME`         | The name of the file (or use `&NAMEL` for lowercase)                              |
| `&EXT`          | The extension of the file (or use `&EXTL` for lowercase)                          |

### Other

| Variable        | Description                                                                       |
| --------------- | --------------------------------------------------------------------------------- |
| `&USERNAME`     | Connected username. Can also use `{usrprf}`                                       |
| `&HOST`         | Connected hostname. Can also use `{host}`                                         |
| `&HOME`         | Current home directory. Typically not the same as deploy directory.               |
| `&BRANCH`       | The current branch name in git. Can also use `{branch}`                           |

## PASE environment variables

When you run Actions in the pase environment, all variables from VS Code (things like `&CURLIB`, `&BUILDLIB`, custom variables, `.env` variables) are inherited into the spawned pase shell.

For example, let's say we had this shell script and this Action:

```sh
echo "Welcome"
echo "The current library is $CURLIB"
```

```json
  {
    "name": "Run my shell script",
    "command": "chmod +x ./myscript.sh && ./myscript.sh",
    "extensions": [
      "GLOBAL"
    ],
    "environment": "pase",
    "deployFirst": true
  }
```

You will see the output:

```txt title="output"
Current library: USERLIB
Library list: QDEVTOOLS SAMPLE
Commands:
  chmod +x ./myscript.sh && ./myscript.sh

Welcome
The current library is USERLIB
```

## Environment file

As well as custom variables defined in the User Library List view, users can also make use of the `.env` file.

The `.env` file allows each developer to define their own configuration. For example, standard development practice with git is everyone developing in their own environment - so developers might build into their own libraries. The `.env` file should always be in the `.gitignore` file.

Variables defined in this file will overwrite any of the default variables provided.

### `actions.json`

```jsonc
// actions.json
[
 {
   "name": "Deploy & build with ibmi-bob 🔨",
   "command": "error=*EVENTF lib1=&DEVLIB makei -f &BASENAME",
   "extensions": [
     "GLOBAL"
   ],
   "environment": "pase",
   "deployFirst": true
 }
]
```

### Developer specific `.env` files

```sh
# developer A:
DEVLIB=DEVALIB
```

```sh
# developer B:
DEVLIB=DEVBLIB
```

### Branch library

`&BRANCHLIB` is a special variable for generating a library name based on the branch name. The Source Orbit tool also supports this same branch library name logic.

The `&BRANCHLIB` variable will always start with `VS` followed by a deterministic set of 8 characters based on the current branch name.

```jsonc
// actions.json
[
 {
   "name": "Deploy & build with ibmi-bob 🔨",
   "command": "error=*EVENTF lib1=&BRANCHLIB makei -f &BASENAME",
   "extensions": [
     "GLOBAL"
   ],
   "environment": "pase",
   "deployFirst": true
 }
]
```

### `.env` and ILE actions

When you are compiling local sources using `"environment": "ile"`, then it will use the User Library List for the job. You can use the `CURLIB` and `LIBL` variables to override them. This is useful because then it allows project-specific library lists.

```json
[
  {
    "name": "Compile with CRTBNDRPG 🔨",
    "command": "CRTBNDRPG PGM(&CURLIB/&NAME) SRCSTMF('&RELATIVEPATH') OPTION(*EVENTF) DBGVIEW(*SOURCE) TGTRLS(*CURRENT) TGTCCSID(*JOB)",
    "environment": "ile",
    "deployFirst": true,
    "extensions": [
      "RPGLE"
    ]
  }
]
```

```sh
# developer A:
CURLIB=BLDLIB
LIBL=MYDB SAMPLE SYSTOOLS
```
