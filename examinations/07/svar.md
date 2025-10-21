# QUESTION A

Make similar changes to this playbook that we did for the _nginx_ server, so that
the `mariadb` service starts automatically at boot, and is started when the playbook
is run.
```bash
💖claire 💕 🎀📁 ~/ansible 💜💙💫⏰ 13:48 🌸ansible-playbook -v 07-mariadb.yml
Using /home/claire/ansible/ansible.cfg as config file

PLAY [db] ******************************************************************************************************************************

TASK [Gathering Facts] *****************************************************************************************************************
ok: [192.168.121.17]

TASK [Ensure MariaDB-server is installed.] *********************************************************************************************
ok: [192.168.121.17] => {"changed": false, "msg": "Nothing to do", "rc": 0, "results": []}

TASK [Ensure MariaDB service is enabled and started] ***********************************************************************************
changed: [192.168.121.17] => {"changed": true, "enabled": true, "name": "mariadb", "state": "started", "status": {"AccessSELinuxContext": "system_u:object_r:mysqld_unit_file_t:s0", "ActiveEnterTimestampMonotonic": "0", "ActiveExitTimestampMonotonic": "0", "ActiveState": "inactive", "After": "system.slice systemd-tmpfiles-setup.service -.mount basic.target sysinit.target network.target tmp.mount systemd-journald.socket", "AllowIsolate": "no", "AssertResult": "no", "AssertTimestampMonotonic": "0", "Before": "shutdown.target", "BlockIOAccounting": "no", "BlockIOWeight": "[not set]", "CPUAccounting": "yes", "CPUAffinityFromNUMA": "no", "CPUQuotaPerSecUSec": "infinity", "CPUQuotaPeriodUSec": "infinity", "CPUSchedulingPolicy": "0", "CPUSchedulingPriority": "0", "CPUSchedulingResetOnFork": "no", "CPUShares": "[not set]", "CPUUsageNSec": "[not set]", "CPUWeight": "[not set]", "CacheDirectoryMode": "0755", "CanFreeze": "yes", "CanIsolate": "no", "CanReload": "no", "CanStart": "yes", "CanStop": "yes", "CapabilityBoundingSet": "cap_chown cap_dac_override cap_dac_read_search cap_fowner cap_fsetid cap_kill cap_setgid cap_setuid cap_setpcap cap_linux_immutable cap_net_bind_service cap_net_broadcast cap_net_admin cap_net_raw cap_ipc_lock cap_ipc_owner cap_sys_module cap_sys_rawio cap_sys_chroot cap_sys_ptrace cap_sys_pacct cap_sys_admin cap_sys_boot cap_sys_nice cap_sys_resource cap_sys_time cap_sys_tty_config cap_mknod cap_lease cap_audit_write cap_audit_control cap_setfcap cap_mac_override cap_mac_admin cap_syslog cap_wake_alarm cap_block_suspend cap_audit_read cap_perfmon cap_bpf cap_checkpoint_restore", "CleanResult": "success", "CollectMode": "inactive", "ConditionResult": "no", "ConditionTimestampMonotonic": "0", "ConfigurationDirectoryMode": "0755", "Conflicts": "shutdown.target", "ControlGroupId": "0", "ControlPID": "0", "CoredumpFilter": "0x33", "DefaultDependencies": "yes", "DefaultMemoryLow": "0", "DefaultMemoryMin": "0", "Delegate": "no", "Description": "MariaDB 10.5 database server", "DevicePolicy": "auto", "Documentation": "\"man:mariadbd(8)\" https://mariadb.com/kb/en/library/systemd/", "DynamicUser": "no", "ExecMainCode": "0", "ExecMainExitTimestampMonotonic": "0", "ExecMainPID": "0", "ExecMainStartTimestampMonotonic": "0", "ExecMainStatus": "0", "ExecStart": "{ path=/usr/libexec/mariadbd ; argv[]=/usr/libexec/mariadbd --basedir=/usr $MYSQLD_OPTS $_WSREP_NEW_CLUSTER ; ignore_errors=no ; start_time=[n/a] ; stop_time=[n/a] ; pid=0 ; code=(null) ; status=0/0 }", "ExecStartEx": "{ path=/usr/libexec/mariadbd ; argv[]=/usr/libexec/mariadbd --basedir=/usr $MYSQLD_OPTS $_WSREP_NEW_CLUSTER ; flags= ; start_time=[n/a] ; stop_time=[n/a] ; pid=0 ; code=(null) ; status=0/0 }", "ExecStartPost": "{ path=/usr/libexec/mariadb-check-upgrade ; argv[]=/usr/libexec/mariadb-check-upgrade ; ignore_errors=no ; start_time=[n/a] ; stop_time=[n/a] ; pid=0 ; code=(null) ; status=0/0 }", "ExecStartPostEx": "{ path=/usr/libexec/mariadb-check-upgrade ; argv[]=/usr/libexec/mariadb-check-upgrade ; flags= ; start_time=[n/a] ; stop_time=[n/a] ; pid=0 ; code=(null) ; status=0/0 }", "ExecStartPre": "{ path=/usr/libexec/mariadb-prepare-db-dir ; argv[]=/usr/libexec/mariadb-prepare-db-dir mariadb.service ; ignore_errors=no ; start_time=[n/a] ; stop_time=[n/a] ; pid=0 ; code=(null) ; status=0/0 }", "ExecStartPreEx": "{ path=/usr/libexec/mariadb-prepare-db-dir ; argv[]=/usr/libexec/mariadb-prepare-db-dir mariadb.service ; flags= ; start_time=[n/a] ; stop_time=[n/a] ; pid=0 ; code=(null) ; status=0/0 }", "ExitType": "main", "FailureAction": "none", "FileDescriptorStoreMax": "0", "FinalKillSignal": "9", "FragmentPath": "/usr/lib/systemd/system/mariadb.service", "FreezerState": "running", "GID": "[not set]", "Group": "mysql", "GuessMainPID": "yes", "IOAccounting": "no", "IOReadBytes": "18446744073709551615", "IOReadOperations": "18446744073709551615", "IOSchedulingClass": "2", "IOSchedulingPriority": "4", "IOWeight": "[not set]", "IOWriteBytes": "18446744073709551615", "IOWriteOperations": "18446744073709551615", "IPAccounting": "no", "IPEgressBytes": "[no data]", "IPEgressPackets": "[no data]", "IPIngressBytes": "[no data]", "IPIngressPackets": "[no data]", "Id": "mariadb.service", "IgnoreOnIsolate": "no", "IgnoreSIGPIPE": "yes", "InactiveEnterTimestampMonotonic": "0", "InactiveExitTimestampMonotonic": "0", "JobRunningTimeoutUSec": "infinity", "JobTimeoutAction": "none", "JobTimeoutUSec": "infinity", "KeyringMode": "private", "KillMode": "control-group", "KillSignal": "15", "LimitAS": "infinity", "LimitASSoft": "infinity", "LimitCORE": "infinity", "LimitCORESoft": "infinity", "LimitCPU": "infinity", "LimitCPUSoft": "infinity", "LimitDATA": "infinity", "LimitDATASoft": "infinity", "LimitFSIZE": "infinity", "LimitFSIZESoft": "infinity", "LimitLOCKS": "infinity", "LimitLOCKSSoft": "infinity", "LimitMEMLOCK": "8388608", "LimitMEMLOCKSoft": "8388608", "LimitMSGQUEUE": "819200", "LimitMSGQUEUESoft": "819200", "LimitNICE": "0", "LimitNICESoft": "0", "LimitNOFILE": "524288", "LimitNOFILESoft": "1024", "LimitNPROC": "1523", "LimitNPROCSoft": "1523", "LimitRSS": "infinity", "LimitRSSSoft": "infinity", "LimitRTPRIO": "0", "LimitRTPRIOSoft": "0", "LimitRTTIME": "infinity", "LimitRTTIMESoft": "infinity", "LimitSIGPENDING": "1523", "LimitSIGPENDINGSoft": "1523", "LimitSTACK": "infinity", "LimitSTACKSoft": "8388608", "LoadState": "loaded", "LockPersonality": "no", "LogLevelMax": "-1", "LogRateLimitBurst": "0", "LogRateLimitIntervalUSec": "0", "LogsDirectoryMode": "0755", "MainPID": "0", "ManagedOOMMemoryPressure": "auto", "ManagedOOMMemoryPressureLimit": "0", "ManagedOOMPreference": "none", "ManagedOOMSwap": "auto", "MemoryAccounting": "yes", "MemoryAvailable": "infinity", "MemoryCurrent": "[not set]", "MemoryDenyWriteExecute": "no", "MemoryHigh": "infinity", "MemoryLimit": "infinity", "MemoryLow": "0", "MemoryMax": "infinity", "MemoryMin": "0", "MemorySwapMax": "infinity", "MountAPIVFS": "no", "NFileDescriptorStore": "0", "NRestarts": "0", "NUMAPolicy": "n/a", "Names": "mariadb.service", "NeedDaemonReload": "no", "Nice": "0", "NoNewPrivileges": "no", "NonBlocking": "no", "NotifyAccess": "main", "OOMPolicy": "stop", "OOMScoreAdjust": "0", "OnFailureJobMode": "replace", "OnSuccessJobMode": "fail", "Perpetual": "no", "PrivateDevices": "no", "PrivateIPC": "no", "PrivateMounts": "no", "PrivateNetwork": "no", "PrivateTmp": "yes", "PrivateUsers": "no", "ProcSubset": "all", "ProtectClock": "no", "ProtectControlGroups": "no", "ProtectHome": "no", "ProtectHostname": "no", "ProtectKernelLogs": "no", "ProtectKernelModules": "no", "ProtectKernelTunables": "no", "ProtectProc": "default", "ProtectSystem": "no", "RefuseManualStart": "no", "RefuseManualStop": "no", "ReloadResult": "success", "ReloadSignal": "1", "RemainAfterExit": "no", "RemoveIPC": "no", "Requires": "sysinit.target system.slice -.mount", "RequiresMountsFor": "/var/tmp", "Restart": "on-abort", "RestartKillSignal": "15", "RestartUSec": "5s", "RestrictNamespaces": "no", "RestrictRealtime": "no", "RestrictSUIDSGID": "no", "Result": "success", "RootDirectoryStartOnly": "no", "RuntimeDirectoryMode": "0755", "RuntimeDirectoryPreserve": "no", "RuntimeMaxUSec": "infinity", "RuntimeRandomizedExtraUSec": "0", "SameProcessGroup": "no", "SecureBits": "0", "SendSIGHUP": "no", "SendSIGKILL": "no", "Slice": "system.slice", "StandardError": "inherit", "StandardInput": "null", "StandardOutput": "journal", "StartLimitAction": "none", "StartLimitBurst": "5", "StartLimitIntervalUSec": "10s", "StartupBlockIOWeight": "[not set]", "StartupCPUShares": "[not set]", "StartupCPUWeight": "[not set]", "StartupIOWeight": "[not set]", "StateChangeTimestampMonotonic": "0", "StateDirectoryMode": "0755", "StatusErrno": "0", "StopWhenUnneeded": "no", "SubState": "dead", "SuccessAction": "none", "SyslogFacility": "3", "SyslogLevel": "6", "SyslogLevelPrefix": "yes", "SyslogPriority": "30", "SystemCallErrorNumber": "2147483646", "TTYReset": "no", "TTYVHangup": "no", "TTYVTDisallocate": "no", "TasksAccounting": "yes", "TasksCurrent": "[not set]", "TasksMax": "2437", "TimeoutAbortUSec": "5min", "TimeoutCleanUSec": "infinity", "TimeoutStartFailureMode": "terminate", "TimeoutStartUSec": "5min", "TimeoutStopFailureMode": "terminate", "TimeoutStopUSec": "5min", "TimerSlackNSec": "50000", "Transient": "no", "Type": "notify", "UID": "[not set]", "UMask": "0007", "UnitFilePreset": "disabled", "UnitFileState": "disabled", "User": "mysql", "UtmpMode": "init", "WatchdogSignal": "6", "WatchdogTimestampMonotonic": "0", "WatchdogUSec": "infinity"}}

PLAY RECAP *****************************************************************************************************************************
192.168.121.17             : ok=3    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```

# QUESTION B

When you have run the playbook above successfully, how can you verify that the `mariadb`
service is started and is running?
[vagrant@dbserver ~]$ systemctl status mariadb
● mariadb.service - MariaDB 10.5 database server
     Loaded: loaded (/usr/lib/systemd/system/mariadb.service; enabled; preset: >
     Active: active (running) since Tue 2025-10-21 11:48:26 UTC; 8min ago
       Docs: man:mariadbd(8)
             https://mariadb.com/kb/en/library/systemd/
    Process: 5693 ExecStartPre=/usr/libexec/mariadb-check-socket (code=exited, >
    Process: 5715 ExecStartPre=/usr/libexec/mariadb-prepare-db-dir mariadb.serv>
    Process: 5812 ExecStartPost=/usr/libexec/mariadb-check-upgrade (code=exited>
   Main PID: 5797 (mariadbd)
     Status: "Taking your SQL requests now..."
      Tasks: 8 (limit: 2437)
     Memory: 83.3M
        CPU: 735ms
     CGroup: /system.slice/mariadb.service
             └─5797 /usr/libexec/mariadbd --basedir=/usr
lines 1-15/15 (END)

Man göra det genom ssh eller direkt på servern med hjälp av `systemctl status mariadb`, och då ser det ut som det är ovanför. Eller så kan man använda sig av modulen ansible.builtin.command och då ser det ut så här.

💖claire 💕 🎀📁 ~/ansible 💜💙💫⏰ 13:58 🌸ansible db -m ansible.builtin.command -a "systemctl status mariadb"
192.168.121.17 | CHANGED | rc=0 >>
● mariadb.service - MariaDB 10.5 database server
     Loaded: loaded (/usr/lib/systemd/system/mariadb.service; enabled; preset: disabled)
     Active: active (running) since Tue 2025-10-21 11:48:26 UTC; 25min ago
       Docs: man:mariadbd(8)
             https://mariadb.com/kb/en/library/systemd/
    Process: 5693 ExecStartPre=/usr/libexec/mariadb-check-socket (code=exited, status=0/SUCCESS)
    Process: 5715 ExecStartPre=/usr/libexec/mariadb-prepare-db-dir mariadb.service (code=exited, status=0/SUCCESS)
    Process: 5812 ExecStartPost=/usr/libexec/mariadb-check-upgrade (code=exited, status=0/SUCCESS)
   Main PID: 5797 (mariadbd)
     Status: "Taking your SQL requests now..."
      Tasks: 8 (limit: 2437)
     Memory: 83.3M
        CPU: 861ms
     CGroup: /system.slice/mariadb.service
             └─5797 /usr/libexec/mariadbd --basedir=/usr

💖claire 💕 🎀📁 ~/ansible 💜💙💫⏰ 14:13 🌸


# BONUS QUESTION

How many different ways can use come up with to verify that the `mariadb` service is running?
De två innan och sen kan man göra yml-fil för att se att mariadb lyssnar på rätt port eller också ansible.builtin.shell. Det agerar som command-modulen men har lite mer avancerade kommandos.

