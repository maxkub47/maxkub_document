---
title: Tricks
sidebar_position: 4
---


### Comparing sources

Compare two sources, whether they are members or streamfiles.

1. right click on either type, choose 'Select for compare'
2. right click the other source you'd like to compare with and choose 'Compare with Selected'

![assets/compare_01.png](../img/compare_01.png)

### Running SQL statement

Install the [Db2 for IBM i extension](https://marketplace.visualstudio.com/items?itemName=HalcyonTechLtd.vscode-db2i) for this functionality. [Check out the documentation here](../extention/db2).

It is also possible to run SQL statements right from the editor in an SQL file. You can either highlight the statement you want to run or move your anchor over the statement and use Ctrl+R/Cmd+R to execute the statement.

SQL result sets appear in the 'IBM i: Results' panel.

![assets/db_03.png](../img/db_03.png)

### Search source files and IFS directories

Right click and click 'Search' on IFS directories and source files to search through the content of streamfiles and source members.

### Overtype

VS Code works in "insert" mode. This can be annoying when editing a fixed mode source, for example DDS. Fortunately there is an [Overtype extension](https://marketplace.visualstudio.com/items?itemName=DrMerfy.overtype) that allows you to toggle between insert and  overtype, and can also display the current mode in the status bar.

### Font Size

Font size in the editor is controlled by the VS Code setting *Editor: Font Size*.  However, with your cursor in an editor, you can also temporarily change the editor font size by holding Ctrl and using your mouse scroll bar.

Font size in the Menu, Side, Status and Activity bars can be changed using holding down Ctrl, then using  + or -. Such changes will hold from session to session. However, this will also change the size of the editor font and you may have to adjust it as above for this session.

Rule of thumb: Experiment.