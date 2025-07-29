# PowerShell scripts

If you repeat a task in the same way, automate it. PowerShell can be used to automate tasks through the command prompt. A Windows device includes Windows PowerShell and can be installed on macOS `brew install --cask powershell` and Linux (Ubuntu) `brew install --cask powershell`. __Tips:__ Always test with dummy data first to avoid data loss (use `-WhatIf`).

## File Management Scripts
__What:__ Automate file transfer

__Why:__ No longer will a file have to be manually cut from Downloads and pasted to it's new home. 
```javascript
  $sourceDir = "C:\SourceFolder"
  $destDir = "D:\BackupFolder"
  
  # Ensure destination folder exists
  if (!(Test-Path $destDir)) {
      New-Item -Path $destDir -ItemType Directory
  }
  
  # Get all files in the source folder (excluding subfolders)
  Get-ChildItem -Path $sourceDir -File | ForEach-Object {
      $sourceFile = $_.FullName
      $destinationFile = Join-Path $destDir $_.Name
  
      # Copy the file
      Copy-Item -Path $sourceFile -Destination $destinationFile -Force
  
      # Confirm copy, then delete original
      if (Test-Path $destinationFile) {
          Remove-Item -Path $sourceFile -Force
          Write-Output "Moved file: $($_.Name)"
      } else {
          Write-Warning "Failed to copy file: $($_.Name)"
      }
  }
```
