---
title: Global
sidebar_position: 2
---



These are setting  which affect the extension (and therefore *every* connection). To adjust the extension's global setting, either:

- Use the standard VS Code <kbd>Ctrl</kbd> + <kbd>,</kbd> and click Extensions
- or click File/Preferences/Settings and click Extensions
- or press <kbd>F1</kbd>, search for `Preferences: Open Settings (UI)` and click Extensions.

Settings for the extension will be under `Code for IBM i`

Most of the setting have a self explanatory description. A few have notes below.

**It is not recommended editing the JSON manually. If you do, restart/reload VS Code so Code for IBM i can pickup the changes.**

![assets/settings_01.png](../img/settings_01.png)

---

### IFS deletion warning (Safe delete)

If enabled, when the user tries to delete a directory, they will be asked to confirm the deletion by typing in the directory's name.

![](../img/safeDelete.png)

### Actions

Actions can be edited in settings.json, but also more easily by clicking **Actions** in the status bar. See *Actions*, above.

### Connections

Connections can be edited in settings.json, but you'd typically add additional connections as in *Connect First Time*, above.

You may use the following variables in any of the strings within Connections:
- `${userHome}` = replaced with the user's home directory.
- `${pathSeparator}` = replaced with the path separator.  (Typically "\\" on Windows or "/" on Mac/Unix/Linux.)

### Connection Settings

These are the various setting relating to the items in the browsers, e.g., the list of source files in the OBJECT BROWSER. While these can be edited in settings.json, most can be more easily maintained by clicking or right clicking on an item in the browser.

### Log Compile Output

When enabled, spool files will be logged from the command execution.
These spool files can be found under the **Output** tab (View->Output, or Ctrl + Shift + U). Select **IBM i Output** in the drop down on the right.

![Panel on Right](../img/LogOutput_01.png)

You can clear the Output tab using the **Clear Output** icon on the right.

![Clear output](../img/LogOutput_02.png)

You can change the font size in the OUTPUT tab in your settings.json thus:

```json
"[Log]": {
    "editor.fontSize": 11
},
```
