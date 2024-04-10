---
title: Execution
sidebar_position: 3
---

import Tabs from "@theme/Tabs";
import TabItem from "@theme/TabItem";

There are four varieties of Actions:

- if type is `file` and 'deploy first' is enabled, deploy the workspace, then:
- execute immediately,
- or they can be displayed for modification,
- or they can be prompted through the user interface.

## Execute Immediately

If we have a "**Call program**" command with a "Command to run" string like this:

```CL
CALL &LIBRARY/&NAME
```

It will execute immediatly it is selected.

## Display for modification

If the "Command to run" string has a leading `?` like `?CALL &LIBRARY/&NAME`, then the command is displayed and editable before command is executed.

![Action Displayed for Modification](../img/actions_exec_01.png)

For example, you might want to add `PARM('Douglas' 'Adams')` to the end.

![Modified Action](../img/actions_exec_02.png)

## Prompted

Rather than using the "?", you can have the Action prompt for values.
The "Command to run" string can have embedded prompt string(s) to invoke prompting.

A "prompt string" has the format `${NAME|LABEL|[DEFAULTVALUE]}` where:

- NAME is an arbitrary name for the prompt field, but must be unique for this action.
- LABEL is the text to describe the prompt field.
- [DEFAULTVALUE] is an **optional** value to pre-populate the prompt field.

---

### Examples

<Tabs>
<TabItem label="Example 1" value="Example 1">
Suppose we have a "**Call program, prompt for parms**" action with the "Command to run" defined like this:

```CL
CALL &LIBRARY/&NAME PARM('${AAA|First name|Your name}' '${xyz|Last Name}')
```

If we run the action it prompts like this:

![Prompting Action Example 1](../img/actions_exec_03.png)

If we complete the screen like this:

and click **Execute** a command like this is executed;

```CL
CALL LENNONS1/ATEST PARM('Douglas' 'Adams')
```

![Completed Prompted Action](../img/actions_exec_04.png)

</TabItem>
<TabItem label="Example 2" value="Example 2">
You can also use variables in the prompt string. If an action is defined like this:

```CL
CALL &LIBRARY/&NAME PARM('${AAA|Library|&CURLIB}' '${xyz|Report Name}')
```

&CURLIB will be substituted and the prompt will look like this when executed:

![Prompted Action Example 2](../img/actions_exec_05.png)

</TabItem>
<TabItem label="Example 3" value="Example 3">
Here's a more complex example of a "**Run CRTBNDRPG (inputs)**" action.
The 'Command to run" string is defined like this:

```CL
CRTBNDRPG PGM(${buildlib|Build library|&BUILDLIB}/${objectname|Object Name|&NAME}) SRCSTMF('${sourcePath|Source path|&FULLPATH}') OPTION(*EVENTF) DBGVIEW(*SOURCE) TGTRLS(*CURRENT)
```

When executed, it prompts like this:

![Panel to the right](../img/compile_04.png)

</TabItem></Tabs>
