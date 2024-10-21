# PowerShell Commands Cheatsheet

| Command               | Description                                                                               | Example                                                                |
| --------------------- | ----------------------------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| `Get-Command`         | Gets all commands                                                                         | `Get-Command`                                                          |
| `Get-Help`            | Displays help information for commands                                                    | `Get-Help Get-Command`                                                 |
| `Get-Process`         | Gets the processes that are running on the local computer                                 | `Get-Process`                                                          |
| `Get-Service`         | Gets the status of services on a local or remote computer                                 | `Get-Service`                                                          |
| `Start-Service`       | Starts a stopped service                                                                  | `Start-Service -Name "wuauserv"`                                       |
| `Stop-Service`        | Stops a running service                                                                   | `Stop-Service -Name "wuauserv"`                                        |
| `Restart-Service`     | Restarts a service                                                                        | `Restart-Service -Name "wuauserv"`                                     |
| `Set-ExecutionPolicy` | Changes the user preference for the PowerShell script execution policy                    | `Set-ExecutionPolicy RemoteSigned`                                     |
| `Get-EventLog`        | Gets the events in the event log on the local or remote computers                         | `Get-EventLog -LogName "System"`                                       |
| `New-Item`            | Creates a new item (file, directory, registry key, etc.)                                  | `New-Item -Path "C:\temp\newfile.txt" -ItemType "File"`                |
| `Remove-Item`         | Deletes files and directories                                                             | `Remove-Item -Path "C:\temp\newfile.txt"`                              |
| `Copy-Item`           | Copies an item from one location to another                                               | `Copy-Item -Path "C:\temp\file.txt" -Destination "C:\backup\file.txt"` |
| `Move-Item`           | Moves an item from one location to another                                                | `Move-Item -Path "C:\temp\file.txt" -Destination "C:\backup\file.txt"` |
| `Rename-Item`         | Renames an item                                                                           | `Rename-Item -Path "C:\temp\file.txt" -NewName "newfile.txt"`          |
| `Get-Content`         | Gets the content of the item at the specified location                                    | `Get-Content -Path "C:\temp\file.txt"`                                 |
| `Set-Content`         | Writes or replaces the content in an item with new content                                | `Set-Content -Path "C:\temp\file.txt" -Value "New content"`            |
| `Add-Content`         | Appends content to the specified items                                                    | `Add-Content -Path "C:\temp\file.txt" -Value "Additional content"`     |
| `Clear-Content`       | Deletes the contents of an item, but does not delete the item                             | `Clear-Content -Path "C:\temp\file.txt"`                               |
| `Get-ChildItem`       | Gets the items and child items in one or more specified locations                         | `Get-ChildItem -Path "C:\temp"`                                        |
| `Get-Location`        | Gets information about the current working location or a location stack                   | `Get-Location`                                                         |
| `Set-Location`        | Sets the current working location to a specified location                                 | `Set-Location -Path "C:\temp"`                                         |
| `Invoke-Command`      | Runs commands on local and remote computers                                               | `Invoke-Command -ScriptBlock { Get-Process }`                          |
| `Import-Module`       | Adds one or more modules to the current session                                           | `Import-Module -Name "ActiveDirectory"`                                |
| `Export-ModuleMember` | Specifies the module members that are exported                                            | `Export-ModuleMember -Function "Get-MyFunction"`                       |
| `Get-Module`          | Gets the modules that have been imported or that can be imported into the current session | `Get-Module -ListAvailable`                                            |
| `Remove-Module`       | Removes modules from the current session                                                  | `Remove-Module -Name "ActiveDirectory"`                                |
| `Get-Variable`        | Gets the PowerShell variables in the current console                                      | `Get-Variable`                                                         |
| `Set-Variable`        | Sets the value of a variable                                                              | `Set-Variable -Name "MyVar" -Value "MyValue"`                          |
| `Remove-Variable`     | Deletes a variable and its value                                                          | `Remove-Variable -Name "MyVar"`                                        |
| `Write-Output`        | Sends the specified objects to the next command in the pipeline                           | `Write-Output "Hello, World!"`                                         |
| `Write-Host`          | Displays objects in the host program                                                      | `Write-Host "Hello, World!"`                                           |
| `Read-Host`           | Reads a line of input from the console                                                    | `$input = Read-Host "Enter your name"`                                 |
| `Start-Job`           | Starts a PowerShell background job                                                        | `Start-Job -ScriptBlock { Get-Process }`                               |
| `Get-Job`             | Gets the Windows PowerShell background jobs that are running in the current session       | `Get-Job`                                                              |
| `Stop-Job`            | Stops a PowerShell background job                                                         | `Stop-Job -Id 1`                                                       |
| `Receive-Job`         | Gets the results of a PowerShell background job                                           | `Receive-Job -Id 1`                                                    |
| `Remove-Job`          | Deletes a PowerShell background job                                                       | `Remove-Job -Id 1`                                                     |

## PowerShell Variable Assignments

| Description                           | Example                                                 |
| ------------------------------------- | ------------------------------------------------------- |
| Assign a variable                     | `$myVariable = "Hello, World!"`                         |
| Assign multiple variables in one line | `$var1 = "Hello"; $var2 = "World"; $var3 = 42`          |
| Flip (swap) variables                 | `$temp = $a; $a = $b; $b = $temp`                       |
| Strongly typed variable               | `[int]$myInt = 42; [string]$myString = "Hello, World!"` |

## PowerShell Arrays and Objects

| Description                  | Example                                                         |
| ---------------------------- | --------------------------------------------------------------- |
| Array of strings             | `$array = @("one", "two", "three")`                             |
| Empty array                  | `$emptyArray = @()`                                             |
| Sixth array element          | `$sixthElement = $array[5]`                                     |
| Last three array elements    | `$lastThreeElements = $array[-3..-1]`                           |
| Elements at index 1, 4, 6-9  | `$selectedElements = $array[1, 4, 6..9]`                        |
| Add to array item value      | `$array += "four"`                                              |
| Two arrays into single array | `$combinedArray = $array1 + $array2`                            |
| Create custom object         | `$person = [PSCustomObject]@{FirstName="John"; LastName="Doe"}` |
| Date property of object      | `$currentDate = (Get-Date).Date`                                |

## PowerShell Flow Control

| Description       | Example                                                |
| ----------------- | ------------------------------------------------------ |
| If-Else Statement | `if ($condition) { } elseif ($condition) { } else { }` |
| While Loop        | `while ($condition) { }`                               |
| For Loop          | `for ($i=0; $i -lt 10; $i++) { }`                      |
| Foreach Loop      | `foreach ($file in Get-ChildItem C:\) { $file.Name }`  |
| Pipeline Foreach  | `1..10 \| ForEach-Object { $_ }`                       |
