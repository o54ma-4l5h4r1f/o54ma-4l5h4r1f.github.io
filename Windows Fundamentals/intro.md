---
sort : 2
---

# Intro

Big thanks to [HTB Academy](https://academy.hackthebox.com/)

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

## Windows Directory Structure

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

## Windows File System

There is 5 types : 
* `FAT12` & `FAT16` (both deprecated), `FAT32`, `NTFS`, and `exFAT`.

**FAT** = File Allocation Table
- Used in : SD Cards  / USBs / and to format hard drives.
- 32 == identifying the data cluster on the storage account. 

*FAT32 Cons* 
- Can only be used with files that are less than 4GB.
- No built-in data protection or file compression features.
- Must use third-party tools for file encryption

**NTFS** = New Technology File System 
- The default win file sys type **currently**

## Permissions

### Basic

|     Permission Type    |     Description    |
|---|---|
|Full Control| Allows reading, writing, **changing**, deleting of files/folders.|
|Modify| Allows reading, writing, and deleting of files/folders.|
|List Folder Contents| Allows for **viewing** and **listing** folders and subfolders as well as **executing** files. <br> *Folders only inherit this permission.*|
|Read and Execute| Allows for viewing and listing files and subfolders as well as executing files. <br> *Files and folders inherit this permission*.|
| Write| Allows for **adding** files to folders and subfolders and **writing** to a file.|
| Read | Allows for **viewing** and **listing** of folders and subfolders and **viewing** a file's contents.|


### Advanced

|     Permission    |     Description    |
|---|---|
|     Full control    |     Users are   permitted or denied permissions to add, edit, move, delete files &   folders as well as change NTFS permissions that apply to all permitted   folders    |
|     Traverse folder / execute file    |     Users are   permitted or denied permissions to access a subfolder within a directory   structure even if the user is denied access to contents at the parent folder   level. Users may also be permitted or denied permissions to execute programs    |
|     List folder/read data    |     Users are   permitted or denied permissions to view files and folders contained in the   parent folder. Users can also be permitted to open and view files    |
|     Read attributes    |     Users are   permitted or denied permissions to view basic attributes of a file or folder.   Examples of basic attributes: system, archive, read-only, and hidden    |
|     Read extended attributes    |     Users are   permitted or denied permissions to view extended attributes of a file or   folder. Attributes differ depending on the program    |
|     Create files/write data    |     Users are   permitted or denied permissions to create files within a folder and make   changes to a file    |
|     Create folders/append data    |     Users are   permitted or denied permissions to create subfolders within a folder. Data   can be added to files but pre-existing content cannot be overwritten    |
|     Write attributes    |     Users are   permitted or denied to change file attributes. This permission does not grant   access to creating files or folders    |
|     Write extended attributes    |     Users are   permitted or denied permissions to change extended attributes on a file or   folder. Attributes differ depending on the program    |
|     Delete subfolders and files    |     Users are   permitted or denied permissions to delete subfolders and files. Parent   folders will not be deleted    |
|     Delete    |     Users are   permitted or denied permissions to delete parent folders, subfolders and   files.    |
|     Read permissions    |     Users are   permitted or denied permissions to read permissions of a folder    |
|     Change permissions    |     Users are   permitted or denied permissions to change permissions of a file or folder    |
|     Take ownership    |     Users are   permitted or denied permission to take ownership of a file or folder. The   owner of a file has full permissions to change any permissions    |