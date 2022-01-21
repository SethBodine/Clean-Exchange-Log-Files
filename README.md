# Clean-Exchange-Log-Files

- PowerShell script taken and adapted from [Edward Van Biljon](https://social.technet.microsoft.com/profile/edward+van+biljon) (was on his Technet Gallery, which has been decommissioned in 2020 (original link: *gallery.technet.microsoft.com/office/Clear-Exchange-2013-Log-71abba44*) with the following modifications:

- No need to modify the IIS and Exchange Path => the script uses environment variables to find the Exchange Logging and IIS Logging paths (script has to be used on Exchange servers to remove the log files)

- added -DoNotDelete switch to just assess the amount of files that we'd potentially remove

- added -NoConfirmation switch to avoir being prompted to continue or cancel

- added progress bars

- added script log file

- added compress before delete 

- added version checks - at launch, and during execution it will indicate if a new version is available.

- added an option to log to the working folder
# Usage 

Will display the folders, compress all files older than 2 days in the IIS folder and Exchange Logging directories, and delete all ZIP files older than than 30 days in the same paths
```powershell

.\CleanExchangeLogFiles.ps1 -Days 30 -DeleteLodCTRBackup -ZipDays 2

```
You'll see the progress bars (one for the folder it's cleaning, and one for the files it's cleaning for each folder):

# Usage on a Windows Scheduled task

> NOTE: to use in a Windows Scheduled task, use the `-NoConfirmation` switch to bypass the Confirm Yes/No dialog box. Otherwise the script will just wait for a user input, which will never come because it's a Windows Scheduled task, most likely configured as "non interactive" because we want it to be automatic.
 
In that case, use the -NoConfirmation switch:

```powershell
.\CleanExchangeLogFiles -Days 30 -ZipDays 2 -NoConfirmation
```

This will launch the script in files deletion mode immediately, without the need of a user interaction.


# Log file

The script log file will be located on the user's Documents folder, or if LogHere is specified, the start in folder.