---
sort : 3
---


# Windows powershell 

Powershell is the Windows Scripting Language and shell environment that is built using the .NET framework.

This also allows Powershell to execute .NET functions directly from its shell. Most Powershell commands, called `cmdlets`, are written in `.NET`. Unlike other scripting languages and shell environments, the output of these cmdlets are `objects` — making Powershell `somewhat object oriented`. This also means that running cmdlets allows you to perform actions on the output object(which makes it convenient to pass output from one cmdlet to another). The normal format of a cmdlet is represented using `Verb-Noun`; for example the cmdlet to list commands is called `Get-Command`.

Common verbs to use include:
```powershell
Get
Start
Stop
Read
Write
New
Out
Select
Update
Remove
Invoke
Import
Enable
Disable
...
...
```



## PowerShell ISE ?? 

The Windows PowerShell Integrated Scripting Environment (ISE) is a host application for Windows PowerShell, In the ISE, you can run commands and write, test, and debug scripts in a single Windows-based graphic user interface. 

* someting like an IDE for powershell ^^ 

Powershell scripts extention : `script.ps1` 


## Powershell from cmd ??

```powershell
C:\Windows\system32> powershell

C:\Windows\system32> powershell -c "...." 
```


<kbd>Windows</kbd> + search for pwershell + <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>Enter</kbd> to run it as Administrator.




## Basic Powershell Commands

`Get-Command` and `Get-Help` are our best friends!

```powershell
# To get help about a particular command/cmdlet
> Get-Help Command-Name


# To show somw examples
> Get-Help Command-Name -Examples
> Get-Help Command-Name -Online

# Download the newest help files for PowerShell modules
> Update-Help
```

OR

```powershell
> Command-Name -?
```


`Get-Command` With pattern matching :

```powershell
# Get-Command Verb-*
> Get-Command Get-*


# Get-Command *-Noun
> Get-Command *-Command
> Get-Command *-*req*

CommandType     Name                 Version    Source
-----------     ----                 -------    ------
Cmdlet          Invoke-WebRequest    3.1.0.0    Microsoft.PowerShell.Utility
```



## Object Manipulation

the output of every cmdlet is an object. So to manipulate the output, we need to figure out a few things:

    * passing output to other cmdlets
    * using specific object cmdlets to extract information

The Pipeline`|` is used to pass output from one cmdlet to another

```note
A major difference compared to other shells is that instead of passing text or string to the command after the pipe, powershell passes an object to the next cmdlet.

an object will contain Members of different types such as methods/functions and properties/variables/columnsNames.   
```










view methods and variables with `Get-Member` 

```powershell
# Verb-Noun | Get-Member
> Get-Command | Get-Member

> Get-Command | Get-Member -MemberType Method
```

```note 
One way of manipulating objects is pulling out the properties from the output of a cmdlet and creating a new object. This is done using the `Select-Object` cmdlet.
```









Listing Directories `Get-ChildItem`

```powershell

PS C:\Users\test> Get-ChildItem

PS C:\Users\test> Get-ChildItem -Depth 2 -Hidden



PS C:\Users\osama> Get-ChildItem | Get-Member -MemberType Property


   TypeName: System.IO.DirectoryInfo

Name              MemberType Definition
----              ---------- ----------
Attributes        Property   System.IO.FileAttributes Attributes {get;set;}
CreationTime      Property   datetime CreationTime {get;set;}
CreationTimeUtc   Property   datetime CreationTimeUtc {get;set;}
Exists            Property   bool Exists {get;}
Extension         Property   string Extension {get;}
FullName          Property   string FullName {get;}
LastAccessTime    Property   datetime LastAccessTime {get;set;}
LastAccessTimeUtc Property   datetime LastAccessTimeUtc {get;set;}
LastWriteTime     Property   datetime LastWriteTime {get;set;}
LastWriteTimeUtc  Property   datetime LastWriteTimeUtc {get;set;}
Name              Property   string Name {get;}
Parent            Property   System.IO.DirectoryInfo Parent {get;}
Root              Property   System.IO.DirectoryInfo Root {get;}



PS C:\Users\test> Get-ChildItem | Select-Object -Property Mode,Name

PS C:\Users\test> Get-ChildItem | Select-Object -Property *

# For more 
> Get-Help Select-Object -Examples
<#
 ------- Example 10: Create custom properties on objects -------

    $customObject = 1 | Select-Object -Property MyCustomProperty
    $customObject.MyCustomProperty = "New Custom Property"
    $customObject

    MyCustomProperty
    ----------------
    New Custom Property
#>

```




## Sorting & Filtering Objects


`Sort-Object`

```powershell
>  Get-ChildItem -Path C:\Test -File | Sort-Object -Property Length

>  Get-Process | Sort-Object -Property CPU | Select-Object -Last 5
```


`Where-Object`

```powershell
# Verb-Noun | Where-Object -Property PropertyName -operator Value

> Get-ChildItem | Where-Object -Property Name -Like "*C*"

> Get-ChildItem | Where-Object -Property LastAccessTime -GT "11/2/2022"

> Get-Help Where-Object -Examples
```

below the `$_` operator to iterate through every object passed to the Where-Object cmdlet.

```powershell
# Verb-Noun | Where-Object {$_.PropertyName -operator Value}

> Get-ChildItem | Where-Object {$_.Name -Like "*C*"}

> Get-ChildItem | Where-Object {$_.LastAccessTime -GT "11/2/2022"}
```





## Find a File 

```powershell
> Get-ChildItem -Path C:\ -Include *interesting-file.txt* -File -Recurse -ErrorAction SilentlyContinue
```

## Find Hashes 

```powershell
> Get-FileHash -Algorithm MD5 "C:\file.txt"
```

## Base64 Decode

```powershell
certutil -decode "C:\Users\Administrator\Desktop\b64.txt" decode.txt
```




## Powershell Aliases

```powershell
> Get-Alias

> Get-Command *Alias*

CommandType     Name                                               
-----------     ----                                               
Cmdlet          Export-Alias                                       
Cmdlet          Get-Alias                                          
Cmdlet          Import-Alias                                       
Cmdlet          New-Alias                                          
Cmdlet          Set-Alias                                          
```





> common aliases 

```powershell
cat :: gc :: Get-Content
pwd :: gl :: Get-Location 
cd  :: chdir :: sl :: Set-Location

dir :: ls :: Get-ChildItem
mkdir :: md 

del :: rm :: rmdir :: erase :: rd :: ri :: Remove-Item
copy :: cp :: cpi :: Copy-Item
ren :: rni :: Rename-Item
ni :: New-Item
mv :: Move-Item

echo :: Write-Output

clear :: Clear-Host

compare :: diff :: Compare-Object

wget :: curl :: iwr :: Invoke-WebRequest

ps :: Get-Process

where :: Where-Object
sort :: Sort-Object

gcb :: Get-Clipboard
```

## Powershell vs Bash 

```powershell
certutil.exe -?      # --help in bash
```



> Create an alias for a cmdlet

```powershell
> Set-Alias -Name list -Value Get-ChildItem

> Set-Alias -Name np -Value C:\Windows\notepad.exe
```












## OTHERS

```powershell
> (Get-Command -CommandType Cmdlet) | Measure-Object
> (Get-Command -CommandType Cmdlet) | measure
# 
# Count    : 671
# Average  :
# Sum      :
# Maximum  :
# Minimum  :
# Property :

> (Get-Command -CommandType Cmdlet).count
# 671

```
















































## Enumeration

The first step when you have gained initial access to any machine would be to enumerate. We’ll be enumerating the following

```
* 
* basic networking information
* file permissions
* registry permissions
* scheduled and running tasks
* insecure files
```

### Users & Groups

```powershell
> Get-LocalUser
<#
Name               Enabled Description
----               ------- -----------
Administrator      False   Built-in account for administering the computer/domain
DefaultAccount     False   A user account managed by the system.
Guest              False   Built-in account for guest access to the computer/domain
osama              True
WDAGUtilityAccount False   A user account managed and used by the system for Windows Defender Application
#>


> Get-LocalUser | Select-Object -Property *
```

#### Users Security Identifier (`SID`)

A security identifier is used to uniquely identify a security principal or security group. 

Users refer to accounts by the account name, but the operating system internally refers to accounts and processes that run in the security context of the account by using their SIDs.

SIDs are `unique` within their scope (domain or local), and they're never reused.

> Security identifier architecture

https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/manage/understand-security-identifiers#security-identifier-architecture



```powershell
> Get-LocalUser -SID  S-1-5-21-1814239583-675844868-3605079295-1001
<#
Name  Enabled Description
----  ------- -----------
osama True
#>
```

```powershell
> Get-LocalGroup
```


#### Network information

```powershell
> Get-NetIPConfiguration

> Get-NetIPConfiguration -Detailed

> Get-NetIPConfiguration | Select-Object -Property *
```

```powershell
> Get-NetTCPConnection

> Get-NetTCPConnection | where -Property State -Like "*Listen*"

> NETSTAT.EXE -ant
```


#### Applied patches 

```powershell
> Get-HotFix
<#
Source      Description      HotFixID   InstalledBy   InstalledOn
------      -----------      --------   -----------   -----------
O54MA       Update           KB5017026                9/25/2022 12:00:00 AM
O54MA       Update           KB5019311                9/25/2022 12:00:00 AM
O54MA       Security Update  KB5017233                9/25/2022 12:00:00 AM
#>

> Get-Hotfix -Id KB5017026
```

#### Contents of a backup file

```powershell
> Get-ChildItem -Path C:\ -Include *.bak* -File -Recurse -ErrorAction SilentlyContinue

> Get-Content "C:\Program Files (x86)\Internet Explorer\passwords.bak"
```

#### Search for all files containing API_KEY

```powershell
> Get-ChildItem C:\* -Recurse | Select-String -pattern API_KEY
```

#### list all the running processes

```powershell
> Get-Process
```

#### scheduled tasks
```powershell
> Get-ScheduleTask -TaskName new-sched-task
```


#### Who is the owner of the C:\
```powershell
> Get-Acl c:/
<#
Path Owner                       Access
---- -----                       ------
C:\  NT SERVICE\TrustedInstaller NT AUTHORITY\Authenticated Users Allow  AppendData...
#>
```














































## PowerShell Scripting 

###> Ex1 : 
```port.txt
80
22
23
8080
8888
1337
```

```powershell

$system_ports = Get-NetTCPConnection -State Listen

$text_port = Get-Content -Path C:\Users\Administrator\Desktop\ports.txt

foreach($port in $text_port){

    if($port -in $system_ports.LocalPort){
        echo $port
    }
}
```


###>Ex2 :
```powershell
$number = Get-Random -Minimum 1 -Maximum 10
do {
  $guess = Read-Host - "PromptWhat's your guess?"
  if ($guess -lt $number) {
    Write-Output 'Too low!'
  }
  elseif ($guess -gt $number) {
    Write-Output 'Too high!'
  }
}
until ($guess -eq $number)
```



###>Ex3 : 
```powershell
$date = Get-Date -Date 'November 22'
while ($date.DayOfWeek -ne 'Thursday') {
  $date = $date.AddDays(1)
}
Write-Output $date

```


###>Ex4 : 
```powershell
while ($i -lt 5) {
  $i += 1
  if ($i -eq 3) {
    continue
  }
  Write-Output $i
}
```

###>Ex5 : 
```powershell
$number = 1..10
foreach ($n in $number) {
  if ($n -ge 4) {
    Return $n
  }
}
```
























































# PowerShell & Pentesting








```powershell
PS C:\Windows\system32 > Get-ExecutionPolicy
Unrestricted

PS C:\Windows\system32 > Set-ExecutionPolicy Unrestricted

Execution Policy Change
The execution policy helps protect you from scripts that you do not trust. Changing the execution policy might expose
you to the security risks described in the about_Execution_Policies help topic at https:/go.microsoft.com/fwlink/?LinkID=135170. Do you want to change the execution policy?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): Y
```




# Download files 
```powershell

PS C:\Windows\system32 > $URL="http://192.168.0.1/MyFile.txt"
PS C:\Windows\system32 > $OUT="C:\Files\MyFile.txt" 

# 1 
PS C:\Windows\system32 > Invoke-WebRequest -URI $URL -OutFile $OUT 

# 2 
PS C:\Windows\system32 > (New-Object System.Net.WebClient).DownloadFile ($URL, $OUT)

# 3  
PS C:\Windows\system32 > Start-BitsTransfer -Source $URL -Destination $OUT
```


## PowerCat - Netcat ?? 

```powershell

PS C:\Windows\system32 > 
```


> note, How to send a file to a listening connection ??  




## PowerShell with Windows API !!!! 



## new-object in powershell ?? 













## References

* https://tryhackme.com/room/powershell
