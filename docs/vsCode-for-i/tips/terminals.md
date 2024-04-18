---
title: Terminals 
sidebar_position: 3
---


In Code for IBM i you can open a 5250 terminal in it's own tab, so almost all developer needs are integrated into the editor. You can launch either a 5250 terminal or a pase shell right in the editor.

![Screenshot 2021-12-06 at 12 07 22 PM](https://user-images.githubusercontent.com/3708366/144915006-20d44162-23ec-4f04-beec-889f989cd497.png)

_Shows explorer, RPGLE code, problems, outline view and 5250 terminal._

## Terminal Startup

Hover over the connected system in the Status Bar

![System Quick Pick menu](../img/Terminals_01.png)

---

Click  **Terminals** in the quick pick menu, then choose a terminal:

* **PASE** will launch into the pase environment
* **5250** will launch a 5250 emulator to the connected system.

![Choose termimal](../img/Terminals_02.png)

## 5250 Requirements & Settings

To launch a 5250 emulator, you must have tn5250 installed on the remote system. This can be [installed via yum](https://www.seidengroup.com/php-documentation/how-to-set-up-the-ibm-i-open-source-environment/).

After you have installed tn5250, you should be able to launch the 5250 terminal, but if not: before connecting to your server, right-click on the server and choose “Connect and Reload Server Settings.”

Code for IBM i provides additional settings so you can setup your termimal how you like. The most common setting is likely the CCSID mapping configuration, which lets you set the encoding for the terminal.

![image](https://user-images.githubusercontent.com/3708366/144916702-79ba1d15-ab1f-4248-abed-8b19c84715c9.png)

## FAQ

- **Do the function keys work?** Yes.
- **It is possible to do a system request?** Yes. Use Command+C.
- **How do I end my session?** Use the Terminal bin in VS Code.
- **I am stuck with `Cursor in protected area of display.`!** Use Command+A to get attention, then use F12 to go back.
- **What are all the key bindings?** [Check them out here](https://linux.die.net/man/1/tn5250).
