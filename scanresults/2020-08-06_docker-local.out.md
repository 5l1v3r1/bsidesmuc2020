# Scan results

... for a local started docker container

## amicontained
```bash
/tools # ./amicontained 
Container Runtime: docker
Has Namespaces:
	pid: true
	user: false
AppArmor Profile: docker-default (enforce)
Capabilities:
	BOUNDING -> chown dac_override fowner fsetid kill setgid setuid setpcap net_bind_service net_raw sys_chroot mknod audit_write setfcap
Seccomp: filtering
Blocked Syscalls (62):
	SYSLOG SETSID USELIB USTAT SYSFS VHANGUP PIVOT_ROOT _SYSCTL ACCT SETTIMEOFDAY MOUNT UMOUNT2 SWAPON SWAPOFF REBOOT SETHOSTNAME SETDOMAINNAME IOPL IOPERM CREATE_MODULE INIT_MODULE DELETE_MODULE GET_KERNEL_SYMS QUERY_MODULE QUOTACTL NFSSERVCTL GETPMSG PUTPMSG AFS_SYSCALL TUXCALL SECURITY LOOKUP_DCOOKIE CLOCK_SETTIME VSERVER MBIND SET_MEMPOLICY GET_MEMPOLICY KEXEC_LOAD ADD_KEY REQUEST_KEY KEYCTL MIGRATE_PAGES UNSHARE MOVE_PAGES PERF_EVENT_OPEN FANOTIFY_INIT NAME_TO_HANDLE_AT OPEN_BY_HANDLE_AT CLOCK_ADJTIME SETNS PROCESS_VM_READV PROCESS_VM_WRITEV KCMP FINIT_MODULE KEXEC_FILE_LOAD BPF USERFAULTFD MEMBARRIER PKEY_MPROTECT PKEY_ALLOC PKEY_FREE RSEQ
Looking for Docker.sock
[2]+  Urgent I/O condition       ./amicontained
```

## botb

```bash
c174797d3e35:/tools# ./botb -metadata -find-docker -find-sockets -find-http
./botb -metadata -find-docker -find-sockets -find-http
[+] Break Out The Box
[+] Looking for Dockerd
[*] Looking for Docker ENV variables
[+] Hunting Docker Socks
[+] Looking for HTTP enabled Sockets from: /
[*] Attempting to query metadata endpoint: 'http://169.254.169.254:8080/'
[*] Attempting to query metadata endpoint: 'http://169.254.169.254/'
[*] Attempting to query metadata endpoint: 'http://metadata.google.internal/'
[*] Attempting to query metadata endpoint: 'http://100.100.100.200/'
[*] Attempting to query metadata endpoint: 'https://kubernetes.default'
[+] Hunting Down UNIX Domain Sockets from: /
[+] Finished

```
