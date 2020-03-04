# Windows Misc

## Windows Terminal

split-panes

 Alt+Shift+-, Alt+Shift+= will split horizontally and vertically. Users can now also reorder tabs to shift around various command-line tools.

can be launched from a command prompt using the `wt` command or with 

    wt -d .
    //Opens the Terminal with the default profile in the current working directory.
    
    wt -d . ; new-tab -d C:\ pwsh.exe
    /* The first is running the default profile starting in the current working directory. The second is using the default profile with pwsh.exe as the "commandline" (instead of the default profile’s "commandline") starting in the C:\ directory. */
    
    `wt -p "Windows PowerShell" -d . ; split-pane -V wsl.exe`
    
    /* Opens the Terminal with two panes, split vertically. The top pane is running the profile with the name “Windows Terminal” and the bottom pane is running the default profile using wsl.exe as the `"commandline"` (instead of the default profile’s `"commandline"`). */
    
    wt -d C:\Users\cinnamon\GitHub\WindowsTerminal ; split-pane -p "Command Prompt" ; split-pane -p "Ubuntu" -d \\wsl$\Ubuntu\home\cinnak -H  // My setup 

![https://devblogs.microsoft.com/commandline/wp-content/uploads/sites/33/2020/02/terminal-command-args.gif](https://devblogs.microsoft.com/commandline/wp-content/uploads/sites/33/2020/02/terminal-command-args.gif)

[WSL](Windows%20Misc/WSL.md)

[Terminal ](Windows%20Misc/Terminal.md)