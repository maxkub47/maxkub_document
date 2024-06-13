---
sidebar_position: 10
title: MaxKuB Summary
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

## Demo Task

- [x] Node.js use Library List  
- [x] Node.js use AS/400 User Profile and Authen
- [x] Node.js use SSL                                                   **[Click](./setup-ssl-ibmi.md)**
- [x] Set start project template for Backend                            **[Click](https://github.com/maxkub47/node_odbc_useibmi_userprofile)**
- [x] Use Nginx in AS/400                                               **[Click](./setup-ssl-ibmi.md#setup-in-nginx)**
- [ ] Example for convert AS/400 to node.js
- [ ] different PHPINFO between APACHEDFT and PHPCOM
- [ ] Set Default Stylesheet in Figma
- [ ] Use Jinkins for IBM i
- [ ] Use CI/CD for IBM i

## AS400 Port inuse

> Path for manual set hosts
<Tabs>
    <TabItem value="window" label="Windows" default>
    "C:\Windows\system32\drivers\etc\hosts"
    </TabItem>
    <TabItem value="macos" label="MacOS">
    "/private/etc/hosts"
    </TabItem>
</Tabs>

---
| Port | description       | PATH                                      |
| :--: | :---------------- | :---------------------------------------- |
|8088|PHPCOM||
|8089|PHPCOM SSL||
| 9100 | Web Service SSL | `http://172.16.1.240:2001/HTTPAdmin`      |
| 9102 | Node JS , EJS     | `/home/max/builds/AS400_MaxTool/ejs-node` |
| 9103 | Maxtool API       | `/home/max/builds/AS400Tool_api`          |
| 9104 | Demo NodeJS       | `/home/max/builds/demo_nodejs`          |
| 9106 | Demo NodeJS nginx       | `/home/max/builds/node_odbc_ibmi_template`          |
| 9191 | NGINX       | `/Qopensys/etc/nginx/nginx.conf`          |

## Save Link

---
get started with node.js [https://developer.ibm.com/learningpaths/get-started-nodejs/]

IBM i Open Source [https://ibmi-oss-docs.readthedocs.io/en/latest/README.html]

VScode Notebook Video [https://www.youtube.com/watch?v=D-AXZZDTQhM&t=1s]
