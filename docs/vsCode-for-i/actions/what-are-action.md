---
title: What are Actions?
sidebar_position: 1
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

An action is used to perform a task on a member, streamfile or other type of object. A comprehensive default set of actions is loaded directly from the extension. You can also easily change or add to actions--see _View/Change/Add Actions_, below.

Actions are defined commands used to perform tasks on members, streamfiles and other types of objects. For example, to compile a source file. Actions can be executed from two different places:

- As you're writing code. For example, to compile a program or module.
- When you right click on a member, streamfile or an object from the OBJECT BROWSER.

A comprehensive set of Actions is provided, but you can add more or change the ones provided.

### Running an Action

To run an Action, open a source member (or IFS streamfile) and press the shortcut key:

<Tabs>
     <TabItem label="Windows" value="Windows">
        > Ctrl + E
    </TabItem>
     <TabItem label="MacOS" value="MacOS">
        > Command + E
    </TabItem>

</Tabs>

This shows a dropdown of the available Actions for the open file. Use the arrow keys to select which Action to run and hit enter to select it.

Example: to run the 'CRTBNDRPG' Action, you must open a source member with either `RPG` or `RPGLE` as the extension. Then, when you use the Run Action shortcut (above), you will see the list of available Actions.

### Working with Actions

<Tabs>
    <TabItem label="View" value="View">
        **Hover over your connection name** in the status bar and when the submenu appears, select Actions to show a list of available Actions.

        - Click on an action to change it.
        - Add actions with New Action.
        - Copy an existing action and modify it with Duplicate.

        ![Action List UI](../img/actions_01.png)

    </TabItem>

    <TabItem label="Add/Change" value="Add/Change">
        Adding or changing Actions shows the same UI.

        In the example we are editing 'Create Bound RPG Program (CRTBNDRPG)'. We can change any of the properties.

        - '**Command to run**' is the command that will be executed. Notice it has portions of text that start with an `&` (ampersand) - such text is a "variable" that will be substituted when the action is run. Commands can have different variables based on what 'Type' (member, streamfile, object) is specified. Note that in addition to the supplied variables, you can create your own variables.  See "Custom Variables", below.

        - '**Extensions**' defines the list of extensions that can use this Action. For `CRTBNDRPG`, that usually means only `RPGLE` and `RPG`, so we would enter: `RPGLE, RPG`.

        - '**Types**' determines which type of object can run this action. For example, if your Action only applies to source members, then choose 'Member' from the dropdown.

        - '**Environment**' determine where the command should be run. In this case, `CRTBNDRPG` needs to run in the ILE environment since it's an ILE command. You also have the option to run commands through PASE or QShell.

        When complete, **click Save**. If you simply close the tab, nothing will be saved.

        ![Action edit UI](../img/actions_02.png)
    </TabItem>

</Tabs>

---

### Actions storage

If you change or add actions as below, then all actions are saved in the `code-for-ibmi.actions` section in `settings.json`. You can also edit the`code-for-ibmi.actions` section manually. If it doesn't exist, you can create you own `code-for-ibmi.actions` section in `settings.json`.

:::warning
When a `code-for-ibmi.actions` section exists in `settings.json` the set of actions is loaded from there, not from the default set in the extension. We don't recommend ending the `settings.json` manually and instead using the Actions view.
:::
