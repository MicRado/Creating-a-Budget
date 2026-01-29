## Get the CSV

<details close>
  <summary>Powershell</summary>

```
    Import-Csv input.csv |
Select-Object Date,
@{ Name="Description"; Expression={ $_.Description -replace "\s-.*$","" } },
Debit,
Balance |
Export-Csv output.csv -NoTypeInformation
```
- \s- → first space followed by -

- .*$ → everything after it to end of line

- Replaces it with nothing → trims cleanly

</details>

<details close>
  <summary>How many cmdlets are installed on the system</summary>

    ```
    Get-Command -CommandType Cmdlet | Measure-Object
```
    
</details>

<details close>
<summary>Get file Hash</summary>

    ```
    Get-FileHash 'C:\Program Files\interesting-file.txt' -Algorithm MD5
```

</details>

<details close>
<summary>request to a web server</summary>

```
Invoke-WebRequest localhost
```

</details>

<details close>
  <summary>Base64 decode the file b64.txt on Windows</summary>

```
$ENCODED = 'agBvAGkAbgBfAHQAaABlAF8AcgBlAGIAZQBsAHMA'
$DECODED = [System.Text.Encoding]::Unicode.GetString([System.Convert]::FromBase64String($ENCODED))
Write-Output $DECODED
```

</details>

<details close>
  <summary>basic invoke-command</summary>

```
Invoke-Command -ComputerName 172.16.5.2 -Credential northdale.lan\peter.mcfae -ScriptBlock { Get-History}
```

</details>

<details close>
  <summary>Compare Files</summary>

```
compare-object (gc file1.txt) (gc file2.txt)
```

</details>

[[Back to top]](#table-of-contents) 

---------------------------------------------------------------------------------------------    
