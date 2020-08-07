# bsidesmuc2020
Created and collected content for BSidesMUC2020



| Service                   | PID  Namesace | User  Namespace | AppArmor Profile/ SELinux | Available  Capabilities | Filtered Seccomp | Metadata-Service                                         | Remark        |
|---------------------------|---------------|-----------------|---------------------------|-------------------------|------------------|----------------------------------------------------------|---------------|
| AWS ECS                   | Yes           | No              | unconfined                | 14                      | 0                | http://169.254.169.254/                                  | -/-           |
| AWS Fargate               | Yes           | No              | unconfined                | 14                      | 65               | None                                                     | -/-           |
| Azure Container Instances | Yes           | No              | unconfined                | 14                      | 65               | None                                                     | -/-           |
| Docker local              | Yes           | No              | docker-default            | 13                      | 62               | None                                                     | Docker Engine |
| fly.io                    | No            | No              | kernel                    | 38                      | disabled         | None                                                     | Firecracker   |
| Google Cloud Run          | No            | No              | unconfined                | 38                      | disabled         | http://169.254.169.254/ http://metadata.google.internal/ | gVisor        |
| Heroku                    | Yes           | No              | lxc-container-default     | 23                      | 47               | None                                                     | LXC           |


Capabilities Comparison

| AWS ECS          | AWS Fargate      | Azure Container  | Docker local     | fly.io           | Google Cloud     | Heroku           |
|------------------|------------------|------------------|------------------|------------------|------------------|------------------|
| chown            | chown            | chown            | chown            | chown            | chown            |                  |
| dac_override     | dac_override     | dac_override     | dac_override     | dac_override     | dac_override     | dac_override     |
|                  |                  |                  |                  | dac_read_search  | dac_read_search  |                  |
| fowner           | fowner           | fowner           | fowner           | fowner           | fowner           | fowner           |
| fsetid           | fsetid           | fsetid           | fsetid           | fsetid           | fsetid           | fsetid           |
| kill             | kill             | kill             | kill             | kill             | kill             | kill             |
| setgid           | setgid           | setgid           | setgid           | setgid           | setgid           | setgid           |
| setuid           | setuid           | setuid           | setuid           | setuid           | setuid           | setuid           |
| setpcap          | setpcap          | setpcap          | setpcap          | setpcap          | setpcap          | setpcap          |
|                  |                  |                  |                  | linux_immutable  | linux_immutable  | linux_immutable  |
| net_bind_service | net_bind_service | net_bind_service | net_bind_service | net_bind_service | net_bind_service | net_bind_service |
|                  |                  |                  |                  | net_broadcast    | net_broadcast    | net_broadcast    |
|                  |                  |                  |                  | net_admin        | net_admin        |                  |
| net_raw          | net_raw          | net_raw          | net_raw          | net_raw          | net_raw          |                  |
|                  |                  |                  |                  | ipc_lock         | ipc_lock         | ipc_lock         |
|                  |                  |                  |                  | ipc_owner        | ipc_owner        | ipc_owner        |
|                  |                  |                  |                  | sys_module       | sys_module       |                  |
|                  |                  |                  |                  | sys_rawio        | sys_rawio        |                  |
| sys_chroot       | sys_chroot       | sys_chroot       | sys_chroot       | sys_chroot       | sys_chroot       |                  |
|                  |                  |                  |                  | sys_ptrace       | sys_ptrace       |                  |
|                  |                  |                  |                  | sys_pacct        | sys_pacct        | sys_pacct        |
|                  |                  |                  |                  | sys_admin        | sys_admin        |                  |
|                  |                  |                  |                  | sys_boot         | sys_boot         |                  |
|                  |                  |                  |                  | sys_nice         | sys_nice         |                  |
|                  |                  |                  |                  | sys_resource     | sys_resource     | sys_resource     |
|                  |                  |                  |                  | sys_time         | sys_time         |                  |
|                  |                  |                  |                  | sys_tty_config   | sys_tty_config   | sys_tty_config   |
| mknod            | mknod            | mknod            | mknod            | mknod            | mknod            |                  |
|                  |                  |                  |                  | lease            | lease            | lease            |
| audit_write      | audit_write      | audit_write      | audit_write      | audit_write      | audit_write      | audit_write      |
|                  |                  |                  |                  | audit_control    | audit_control    | audit_control    |
| setfcap          | setfcap          | setfcap          | setfcap          | setfcap          | setfcap          | setfcap          |
|                  |                  |                  |                  | mac_override     | mac_override     |                  |
|                  |                  |                  |                  | mac_admin        | mac_admin        |                  |
|                  |                  |                  |                  | syslog           | syslog           | syslog           |
|                  |                  |                  |                  | wake_alarm       | wake_alarm       | wake_alarm       |
|                  |                  |                  |                  | block_suspend    | block_suspend    | block_suspend    |
|                  |                  |                  |                  | audit_read       | audit_read       | audit_read       |

Seccomp Filter Comparison

| AWS ECS | AWS Fargate       | Azure Container   | Docker local      | fly.io | Google Cloud | Heroku            |
|---------|-------------------|-------------------|-------------------|--------|--------------|-------------------|
|         | MSGRCV            | MSGRCV            |                   |        |              |                   |
|         | PTRACE            | PTRACE            |                   |        |              | PTRACE            |
|         | SYSLOG            | SYSLOG            |                   |        |              | SYSLOG            |
|         |                   |                   |                   |        |              | SETUID            |
|         |                   |                   |                   |        |              | SETGID            |
|         | SETSID            | SETSID            | SETSID            |        |              | SETSID            |
|         |                   |                   |                   |        |              | SETREUID          |
|         |                   |                   |                   |        |              | SETREGID          |
|         |                   |                   |                   |        |              | SETGROUPS         |
|         |                   |                   |                   |        |              | SETRESUID         |
|         |                   |                   |                   |        |              | SETRESGID         |
|         |                   |                   |                   |        |              | PERSONALITY       |
|         | USELIB            | USELIB            | USELIB            |        |              |                   |
|         | USTAT             | USTAT             | USTAT             |        |              |                   |
|         | SYSFS             | SYSFS             | SYSFS             |        |              |                   |
|         | VHANGUP           | VHANGUP           | VHANGUP           |        |              | VHANGUP           |
|         | PIVOT_ROOT        | PIVOT_ROOT        | PIVOT_ROOT        |        |              | PIVOT_ROOT        |
|         | _SYSCTL           | _SYSCTL           | _SYSCTL           |        |              |                   |
|         |                   |                   |                   |        |              | CHROOT            |
|         | ACCT              | ACCT              | ACCT              |        |              | ACCT              |
|         | SETTIMEOFDAY      | SETTIMEOFDAY      | SETTIMEOFDAY      |        |              | SETTIMEOFDAY      |
|         | MOUNT             | MOUNT             | MOUNT             |        |              |                   |
|         | UMOUNT2           | UMOUNT2           | UMOUNT2           |        |              | UMOUNT2           |
|         | SWAPON            | SWAPON            | SWAPON            |        |              | SWAPON            |
|         | SWAPOFF           | SWAPOFF           | SWAPOFF           |        |              | SWAPOFF           |
|         | REBOOT            | REBOOT            | REBOOT            |        |              | REBOOT            |
|         | SETHOSTNAME       | SETHOSTNAME       | SETHOSTNAME       |        |              | SETHOSTNAME       |
|         | SETDOMAINNAME     | SETDOMAINNAME     | SETDOMAINNAME     |        |              | SETDOMAINNAME     |
|         | IOPL              | IOPL              | IOPL              |        |              |                   |
|         | IOPERM            | IOPERM            | IOPERM            |        |              |                   |
|         | CREATE_MODULE     | CREATE_MODULE     | CREATE_MODULE     |        |              |                   |
|         | INIT_MODULE       | INIT_MODULE       | INIT_MODULE       |        |              | INIT_MODULE       |
|         | DELETE_MODULE     | DELETE_MODULE     | DELETE_MODULE     |        |              | DELETE_MODULE     |
|         | GET_KERNEL_SYMS   | GET_KERNEL_SYMS   | GET_KERNEL_SYMS   |        |              |                   |
|         | QUERY_MODULE      | QUERY_MODULE      | QUERY_MODULE      |        |              |                   |
|         | QUOTACTL          | QUOTACTL          | QUOTACTL          |        |              | QUOTACTL          |
|         | NFSSERVCTL        | NFSSERVCTL        | NFSSERVCTL        |        |              |                   |
|         | GETPMSG           | GETPMSG           | GETPMSG           |        |              |                   |
|         | PUTPMSG           | PUTPMSG           | PUTPMSG           |        |              |                   |
|         | AFS_SYSCALL       | AFS_SYSCALL       | AFS_SYSCALL       |        |              |                   |
|         | TUXCALL           | TUXCALL           | TUXCALL           |        |              |                   |
|         | SECURITY          | SECURITY          | SECURITY          |        |              |                   |
|         | LOOKUP_DCOOKIE    | LOOKUP_DCOOKIE    | LOOKUP_DCOOKIE    |        |              | LOOKUP_DCOOKIE    |
|         | CLOCK_SETTIME     | CLOCK_SETTIME     | CLOCK_SETTIME     |        |              | CLOCK_SETTIME     |
|         | VSERVER           | VSERVER           | VSERVER           |        |              |                   |
|         | MBIND             | MBIND             | MBIND             |        |              |                   |
|         | SET_MEMPOLICY     | SET_MEMPOLICY     | SET_MEMPOLICY     |        |              |                   |
|         | GET_MEMPOLICY     | GET_MEMPOLICY     | GET_MEMPOLICY     |        |              | GET_MEMPOLICY     |
|         | KEXEC_LOAD        | KEXEC_LOAD        | KEXEC_LOAD        |        |              | KEXEC_LOAD        |
|         | ADD_KEY           | ADD_KEY           | ADD_KEY           |        |              | ADD_KEY           |
|         | REQUEST_KEY       | REQUEST_KEY       | REQUEST_KEY       |        |              | REQUEST_KEY       |
|         | KEYCTL            | KEYCTL            | KEYCTL            |        |              | KEYCTL            |
|         | MIGRATE_PAGES     | MIGRATE_PAGES     | MIGRATE_PAGES     |        |              |                   |
|         |                   |                   |                   |        |              | FUTIMESAT         |
|         | UNSHARE           | UNSHARE           | UNSHARE           |        |              | UNSHARE           |
|         | MOVE_PAGES        | MOVE_PAGES        | MOVE_PAGES        |        |              | MOVE_PAGES        |
|         | PERF_EVENT_OPEN   | PERF_EVENT_OPEN   | PERF_EVENT_OPEN   |        |              | PERF_EVENT_OPEN   |
|         | FANOTIFY_INIT     | FANOTIFY_INIT     | FANOTIFY_INIT     |        |              | FANOTIFY_INIT     |
|         | NAME_TO_HANDLE_AT | NAME_TO_HANDLE_AT | NAME_TO_HANDLE_AT |        |              | NAME_TO_HANDLE_AT |
|         | OPEN_BY_HANDLE_AT | OPEN_BY_HANDLE_AT | OPEN_BY_HANDLE_AT |        |              | OPEN_BY_HANDLE_AT |
|         | CLOCK_ADJTIME     | CLOCK_ADJTIME     | CLOCK_ADJTIME     |        |              | CLOCK_ADJTIME     |
|         | SETNS             | SETNS             | SETNS             |        |              | SETNS             |
|         | PROCESS_VM_READV  | PROCESS_VM_READV  | PROCESS_VM_READV  |        |              | PROCESS_VM_READV  |
|         | PROCESS_VM_WRITEV | PROCESS_VM_WRITEV | PROCESS_VM_WRITEV |        |              | PROCESS_VM_WRITEV |
|         | KCMP              | KCMP              | KCMP              |        |              | KCMP              |
|         | FINIT_MODULE      | FINIT_MODULE      | FINIT_MODULE      |        |              | FINIT_MODULE      |
|         | KEXEC_FILE_LOAD   | KEXEC_FILE_LOAD   | KEXEC_FILE_LOAD   |        |              | KEXEC_FILE_LOAD   |
|         | BPF               | BPF               | BPF               |        |              | BPF               |
|         | USERFAULTFD       | USERFAULTFD       | USERFAULTFD       |        |              |                   |
|         | MEMBARRIER        | MEMBARRIER        | MEMBARRIER        |        |              |                   |
|         | PKEY_MPROTECT     | PKEY_MPROTECT     | PKEY_MPROTECT     |        |              |                   |
|         | PKEY_ALLOC        | PKEY_ALLOC        | PKEY_ALLOC        |        |              |                   |
|         | PKEY_FREE         | PKEY_FREE         | PKEY_FREE         |        |              |                   |
|         | IO_PGETEVENTS     | IO_PGETEVENTS     | RSEQ              |        |              |                   |
|         |                   |                   |                   |        |              |                   |

