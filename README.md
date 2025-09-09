# Winget Auto Update Task

This project helps keep your Windows computer safe and up-to-date by automatically running [Winget](https://learn.microsoft.com/en-us/windows/package-manager/winget/) upgrades every time you log in.

The setup is simple: one script creates a **Scheduled Task** in Windows, and another script runs Winget and writes the results to a log file.

---

## Files

- **Setup.ps1**  
  Creates a Task Scheduler folder (`\WingetUpgradeScript`) and a scheduled task called `AutoUpdate`.  
  The task runs **RunWinget.ps1** at every logon.

- **RunWinget.ps1**  
  Runs `winget upgrade --all` with the proper agreement flags.  
  All output (successes and failures) is written to a log file.

---

## Log file

- Location: `C:\tmp\<COMPUTERNAME>.log`  
- Contains entries like:

  `2025-09-08 10:00:01 - Running winget upgrade...`  
  `2025-09-08 10:00:02 - winget: Upgrading Microsoft.Edge`  
  `2025-09-08 10:00:30 - winget: Successfully installed`

  `2025-09-08 10:00:45 - winget: Error 0x80073CF9 while upgrading SomeApp`
  `2025-09-08 10:00:50 - winget upgrade finished.`


---

## How to use

1. Download or clone this repository.

2. Copy both scripts to `C:\tmp\`  
 (or edit `Setup.ps1` if you prefer a different path).

3. Open **PowerShell as Administrator**.

4. Run:
 ```powershell
 Set-ExecutionPolicy Bypass -Scope Process -Force
 .\Setup.ps1
 ```

This will create the Scheduled Task.

The task is stored under Task Scheduler → Task Scheduler Library → WingetUpgradeScript.

Restart your computer or log off/on.
The task will run automatically and log results.

---

## Testing

You don’t need to reboot to test the update script.
Just run this manually: `.\RunWinget.ps1`
This will execute the same logic that the scheduled task uses.

---

## FAQ

Q: Does this script reinstall the scheduled task every time?


A: No. Setup.ps1 only needs to be run once. After that, only RunWinget.ps1 is executed at logon.

Q: What if I want to change the schedule?


A: Open Task Scheduler (taskschd.msc), find the folder WingetUpgradeScript, and edit the AutoUpdate task.

Q: Where is Winget from?


A: Winget is Microsoft’s official package manager for Windows, built into Windows 10 and 11.

---

## Disclaimer

This script is provided as-is. Always review and understand any PowerShell scripts before running them.
You are responsible for changes made to your computer.

---

## Video Tutorial

This project is designed to be beginner-friendly and is accompanied by a YouTube tutorial (link coming soon).
