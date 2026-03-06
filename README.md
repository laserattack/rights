# rights - Linux file permissions explainer

A simple script to explain Linux file permissions in human-readable format

**rights** takes file permissions in various formats (numeric, symbolic, or actual file path) and explains what they mean - who can read, write, execute, and what special bits are set

# Usage

```
What is it : Linux file permissions explainer
Usage      : rights ARGUMENTS

Arguments:
  Symbolic permissions : rwxr-xr-x, rw-------, r-x--x--x
  Numeric permissions  : 755, 644, 777, 600, 444
  File/directory path  : /dev/video0, script.sh, /tmp

Examples:
  rights 755           # Explain numeric permissions
  rights rwxr-xr-x     # Explain symbolic permissions
  rights /dev/video0   # Explain file permissions
```

# Examples

## Explain numeric permissions

```
~
[serr@lap]-> rights 505
File type:           not specified
Special bits:        no suid, no sgid, no sticky
Owner permissions:   read (+4), no write, execute (+1)
Group permissions:   no read, no write, no execute
Others permissions:  read (+4), no write, execute (+1)
Suffix:              not specified
Symbolic:            r-x---r-x
Numeric:             505
```

```
~
[serr@lap]-> rights 5557
File type:           not specified
Special bits:        suid (+4), no sgid, sticky (+1)
Owner permissions:   read (+4), no write, execute with suid (run as file owner) (+1)
Group permissions:   read (+4), no write, execute (+1)
Others permissions:  read (+4), write (+2), sticky (for directories: only file owner or root can delete files) (+1)
Suffix:              not specified
Symbolic:            r-sr-xrwt
Numeric:             5557
```

## Explain symbolic permissions

```
~
[serr@lap]-> rights rwsr-sr-t
File type:           not specified
Special bits:        suid (+4), sgid (+2), sticky (+1)
Owner permissions:   read (+4), write (+2), execute with suid (run as file owner) (+1)
Group permissions:   read (+4), no write, execute with sgid (run as group member) (+1)
Others permissions:  read (+4), no write, sticky (for directories: only file owner or root can delete files) (+1)
Suffix:              not specified
Symbolic:            rwsr-sr-t
Numeric:             7755
```

```
~
[serr@lap]-> rights crw-rw----+
File type:           character device
Special bits:        no suid, no sgid, no sticky
Owner permissions:   read (+4), write (+2), no execute
Group permissions:   read (+4), write (+2), no execute
Others permissions:  no read, no write, no execute
Suffix:              ACL present (Access Control Lists)
Symbolic:            crw-rw----+
Numeric:             660
```

## Explain file permissions

```
~
[serr@lap]-> rights /
File type:           directory
Special bits:        no suid, no sgid, no sticky
Owner permissions:   read (+4), write (+2), execute (+1)
Group permissions:   read (+4), no write, execute (+1)
Others permissions:  read (+4), no write, execute (+1)
Suffix:              not specified
Symbolic:            drwxr-xr-x
Numeric:             755
```

```
~
[serr@lap]-> rights /dev/video0
File type:           character device
Special bits:        no suid, no sgid, no sticky
Owner permissions:   read (+4), write (+2), no execute
Group permissions:   read (+4), write (+2), no execute
Others permissions:  no read, no write, no execute
Suffix:              ACL present (Access Control Lists)
Symbolic:            crw-rw----+
Numeric:             660
```

# Requirements

- Perl 5.10 or newer
- `ls` program (optional for most modes, required for file/directory arguments)