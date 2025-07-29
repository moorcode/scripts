# PowerShell scripts

PowerShell can be used to automate tasks through the command prompt. A Windows device includes Windows PowerShell and can be installed on macOS `brew install --cask powershell` and Linux (Ubuntu) `brew install --cask powershell`. __Tips:__Always test with dummy data first to avoid data loss. Use `-WhatIf`

## File Management Scripts

__Why__: No longer will a file have to be manually cut from the Downloads folder and pasted to it's new home. 
```javascript
  $sourceDir = "C:\SourceFolder"
  $destDir = "D:\BackupFolder"
  
  # Copy all contents
  Copy-Item -Path $sourceDir\* -Destination $destDir -Recurse -Force
  
  # Optional: Check if destination now exists
  if (Test-Path $destDir) {
      # Delete original folder and contents
      Remove-Item -Path $sourceDir -Recurse -Force
      Write-Output "Folder copied and original deleted."
  } else {
      Write-Error "Copy failed. Original folder not deleted."
  }
```
