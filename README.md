# Open WSL here command and context menu option
This guide will help you create a command to open WSL in the current directory and add a right-click context menu option for it.

```cmd
openwslhere
```
![Context menu screenshot](context_menu.jpg "Context menu screenshot")

### How to create a command to open current directory in WSL
> [!NOTE]
> Replace `<your_command_name>` with your desired command name.


---

#### **Option A: If you're using** `PowerShell`

1. Open PowerShell.
2. Run this to open/create your profile file:

```powershell
notepad $PROFILE
```

3. Add this function to the end of the file:

```powershell
function <your_command_name> {
    wsl --cd "$(Get-Location)"
}
```

4. Save and close Notepad.
5. Restart PowerShell.

---

#### **Option B: If you're *still* using** `CMD` *yieks*

1. Open **Notepad**.
2. Paste this code:

```bat
@echo off
wsl --cd "%CD%"
```

3. Save the file as `<your_command_name>.bat` in a folder that's included in your **system PATH**.

### How to add a always visible right-click context menu option to open WSL in the current directory
> [!NOTE]
> Replace `<your_option_description>` with your desired description. (e.g. Open WSL here)

> [!NOTE]
> WSL already has a context menu option to open it in the current directory, but it is only visible when you hold `Shift` and right-click. This guide will add a new option that is always visible and with custom name and icon.

1. Create `.reg` file in any text editor:

```reg
Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\Directory\Background\shell\<your_option_description>]
@="<your_option_description>"
"Icon"="wsl.exe"
"NoWorkingDirectory"=""

[HKEY_CLASSES_ROOT\Directory\Background\shell\<your_option_description>\command]
@="wsl.exe --cd \"%V\""
```
2. Save and double-click it to add it to the registry.
3. Confirm the prompt.