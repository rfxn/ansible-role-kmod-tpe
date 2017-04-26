# ansible-role-kmod-tpe

RHEL/CentOS - Trusted Path Execution Linux Kernel Module

Trusted Path Execution is a security feature that denies users from executing
programs that are not within a root owned path, or optionally the binary itself
root owned, or are world writable or within a world write path. This closes the
door on a whole category of exploits where a malicious user tries to execute his
or her own code to attack the system.

Additionally, this module also provides non-root view restrictions on process list,
kernel modules, kallsyms and calling set(u|g)id.

## Requirements

 - nexcess.repo.elrepo

## Role Variables

Default role variables can be found in 'defaults/main.yml'; supported variables below:

```
# kmod_tpe_lock: True|False
# when enabled, tpe sysctl entries can not be changed without a reboot

# kmod_tpe_log_floodburst: integer, quantative
# number of log entries before logging is disabled

# kmod_tpe_log_floodtime: integer, seconds
# seconds until re-enabling logging after floodburst

# kmod_tpe_log_max: integer, quantitative
# maximun parent processes in a single log entry

# kmod_tpe_log: True|False
# log denied executions

# kmod_tpe_kill: True|False
# kill the offending process and its parent when it gets denied

# kmod_tpe_hardcoded_path: list, full paths
# a list of directories, colon separated, that TPE will be restricted to; nothing outside

# kmod_tpe_paranoid: True|False
# enforce trusted path restrictions on the root

# kmod_tpe_check_file: True|False
# check file owner/mode in addition to directory

# kmod_tpe_strict: True|false
# enforce some TPE features even on trusted users (no world write on exec paths or binaries)

# kmod_tpe_dmz_gid: integer, uid value
# users in this gid can't exec anything at all

# kmod_tpe_admin_gid: integer, uid value
# files belonging to this group are treated as if they're owned by root

# kmod_tpe_trusted_gid: integer, uid value
# gid of trusted users for which TPE is not enforced

# kmod_tpe_trusted_invert: True|False
# inverts trusted_gid from a whitelist to blacklist; only users in trusted_gid
# will have TPE restrictions applied

# kmod_tpe_softmode: True|False
# do not deny any executions, just log what would have been denied.

# kmod_tpe_extras_proc_kallsyms: True|False
# denies non-root users from viewing /proc/kallsyms

# kmod_tpe_extras_ps: True|False
# denies non-root users from viewing processes they don't own

# kmod_tpe_extras_ps_gid: integer, uid value
# gid of users who aren't ps view restricted (wheel gid 10)

# kmod_tpe_extras_lsmod: True|False
# denies non-root users from viewing loaded kernel modules

# kmod_tpe_extras_harden_ptrace: True|False
# denies non-root users from running ptrace operations

# kmod_tpe_extras_harden_symlink: True|False
# denies non-root users from following symlinks to files owned by a different user

# kmod_tpe_extras_harden_hardlinks: True|False
# denies non-root users from creating hardlinks to files owned by other users and special files (devices etc...)

# kmod_tpe_extras_restrict_setuid: True|False
# users not in the trusted_gid are denied calls to setuid
```

## Dependencies

 - nexcess.repo.elrepo

## Example Playbook

    - hosts: servers
      roles:
        - role: nexcess.kmod.tpe
          kmod_tpe_extras_proc_kallsyms: True
          kmod_tpe_extras_ps: True
          kmod_tpe_extras_lsmod: True
          
## License

MIT

## Acknowledgements

 - Corey Henderson - https://github.com/cormander/

Creator and maintainer of kmod-tpe port from grsecurity

 - Brad Spengler - http://grsecurity.net/

Trusted Path Execution is a feature of grsecurity for which code was borrowed from that
project to make this module.

## Author Information
Ryan MacDonald <rmacdonald@nexcess.net> https://github.com/nexcess
	       <ryan@rfxn.com>          https://github.com/rfxn
