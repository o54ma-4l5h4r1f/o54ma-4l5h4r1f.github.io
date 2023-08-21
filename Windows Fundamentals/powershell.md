---
sort : 3
---

# powershell

## Windows Services

> Get-Service 

```powershell
PS> Get-Service 
# Status   Name               DisplayName
# ------   ----               -----------
# Stopped  AarSvc_3eb34       Agent Activation Runtime_3eb34
# Stopped  AarSvc_e0093       Agent Activation Runtime_e0093
# Stopped  AJRouter           AllJoyn Router Service
# Stopped  ALG                Application Layer Gateway Service

PS> Get-Service | ? {$_.Status -eq "Running"}
# Lists all running services


PS> Get-Service | ? {$_.Name -Match "ssh"}
# lists services with a name that contain *ssh* 
```

> sc.exe 

```powershell
PS> sc.exe 

PS> sc.exe query sshd 
# SERVICE_NAME: sshd
#     TYPE               : 10  WIN32_OWN_PROCESS
#     STATE              : 4  RUNNING
#                             (STOPPABLE, NOT_PAUSABLE, IGNORES_SHUTDOWN)
#     WIN32_EXIT_CODE    : 0  (0x0)
#     SERVICE_EXIT_CODE  : 0  (0x0)
#     CHECKPOINT         : 0x0
#     WAIT_HINT          : 0x0
```

