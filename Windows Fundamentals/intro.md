---
sort : 2
---

# Intro

Big thank you to [HTB Academy](https://academy.hackthebox.com/)

## History

Microsoft first introduced the Windows OS on `1985`.

Windows 95 was the first full integration of Windows and DOS and offered built-in Internet support for the first time.

Windows Server was first released in `1993` with the release of Windows NT 3.1 Advanced Server.

With the release of Windows 2000, Microsoft debuted Active Directory + Microsoft Management Console (MMC).

> Versions 

- Windows NT 4
- Windows 2000
- Windows XP
- Windows Server 2003, 2003 R2
- Windows Vista, Server 2008
- Windows 7, Server 2008 R2
- Windows 8, Server 2012
- Windows 8.1, Server 2012 R2
- Windows 10, Server 2016, Server 2019


`Windows NT` is a family of Windows operating systems from 1993 that includes Windows 2000, Vista, 7, 8, 8.1, Windows 10, and now Windows 11

```note
NT = New Technology
```


## Remote Access 

> SSH 

> VPN 

> FTP 

> VNC

> WinRM

> RDP 

- By default, remote access is **not** allowed on Windows operating systems.
- Remote Desktop Files (.rdp)
- RDP Clients :
    
    ```powershell
    PS> mstsc.exe
    ``` 

    ```bash
    $ Xfreerdp /v:$IP /u:$USERNAME /p:$PASSWD
    ```

    ```bash
    $ rdesktop -u $USERNAME $IP
    ```
    
    ```bash
    $ remmina
    ```

<br>
<br>

# Windows Directory Structure

the root directory (boot partition) is `<drive_letter>`:\ (commonly `C` drive)

| Directory | Function |
|-----------------------------------|------------------------|
| Perflogs |  Windows performance logs (empty by default) |
| Program Files | All **16-bit** and **32-bit** programs on `32-bit` systems. <br> Only **64-bit** programs on `64-bit` systems |
| Program Files (x86) | **32-bit** and **16-bit** programs on `64-bit` systems. |
| ProgramData | A _hidden folder_ contains essential data for certain installed programs to run. <br> This data is accessible by the program no matter what user is running it. |
| Users | Contains user profiles for each user that logs onto the system <br> And contains the two folders Public and Default. |
| Default | This is the default user profile template for all created users. |
| Public | This folder is intended for computer users to **share files** and is accessible to all users by default. This folder is shared over the network by default but requires a valid **network account** to access. |
| AppData | Per user application data and settings are stored in a hidden user subfolder (i.e., user.name\AppData). <br> Each of these folders contains three subfolders. <br> - The `Roaming folder` contains machine-independent data that should follow the user's profile, such as custom dictionaries. <br> - The `Local folder` is specific to the computer itself and is never synchronized across the network. <br> - The `LocalLow` is similar to the Local folder, but it has a lower data integrity level. Therefore it can be used, for example,  by a web browser set to protected or safe mode.  |
| Windows | Windows operating system required files. |
| System, System32, SysWOW64 | They Contains all **DLLs** required for the core features of Windows and the Windows API. <br> The operating system searches these folders any time a program asks to load a DLL without specifying an absolute path. |
| WinSxS | The **Windows Component Store** contains a copy of all Windows components, updates, and service packs. |

