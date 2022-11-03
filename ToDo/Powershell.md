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



`Sort-Object`

```powershell
>  Get-ChildItem -Path C:\Test -File | Sort-Object -Property Length

>  Get-Process | Sort-Object -Property CPU | Select-Object -Last 5
```


## Find a File 

```powershell
> Get-ChildItem -Path C:\ -Include *interesting-file.txt* -File -Recurse -ErrorAction SilentlyContinue
```


## Find Hashes 

```powershell
> Get-FileHash -Algorithm MD5 "C:\file.txt"
```







## Powershell vs bash

```powershell

cat -> Get-Content "C:\Program Files\interesting-file.txt"

```





## OTHERS

```powershell
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






















> What is cmdlet ?? 

A cmdlet -- pronounced command-let -- is a small, lightweight `command` that is used in the Windows PowerShell environment. A cmdlet typically exists as a small script that is intended to perform a single specific function such as coping files and changing directories. A cmdlet and its relevant parameters can be entered in a PowerShell command line for immediate execution or included as part of a longer PowerShell script that can be executed as desired.



```note
> ls & dir 

is just an alias of a command-let
```

so how the command-let commands look like ?? 


```powershell
PS C:\Windows\system32 > Get-Alias
```






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
