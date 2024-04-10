---
title: Custom Variables
sidebar_position: 2
---

You can create custom variable to use in your "Command to run" strings. To access custom variables:

Use <kbd>F1</kbd>, then search for "IBM i Custom variables":

![F1 + IBM i Custom Variable](../img/actions_custom_01.png)

---

Or from the User Library List browser:

![Library List Browser](../img/actions_custom_01a.png)

---

In the **Work with Variables** tab, click on **New Variable** to add your variable.

Click on a custom variable to change it or delete it.

![Variables list after Save](../img/actions_custom_04.png)

---

Here we are adding a variable named `&TARGET_RLSE`.

Press Save and the list of custom variables is shown.

![Adding TARGET_RLSE](../img/actions_custom_03.png)

---

#### _Example Usage_

In all the CRTBNDxxx actions add TGTRLS(&TARGET_RLSE), like this:

```CL
?CRTBNDCL PGM(&OPENLIB/&OPENMBR) SRCFILE(&OPENLIB/&OPENSPF) OPTION(*EVENTF) DBGVIEW(*SOURCE)  TGTRLS(&TARGET_RLSE)
```

Now a single change to the TARGET_RLSE custom variable can impact all the CRTBNDxxx actions.
