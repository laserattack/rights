# rights - Linux file permissions explainer

A simple Perl script to explain Linux file permissions in human-readable format

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
~/projects/right
[serr@lap]-> ./rights 505
File type:           not specified
Owner permissions:   read, no write, execute
Group permissions:   no read, no write, no execute
Others permissions:  read, no write, execute
Suffix:              not specified
Symbolic:            r-x---r-x
Numeric:             505
```

```
~/projects/right
[serr@lap]-> rights 5557
File type:           not specified
Owner permissions:   read, no write, execute with suid (run as file owner)
Group permissions:   read, no write, execute
Others permissions:  read, write, sticky bit (for directories: only owner or root can delete files)
Suffix:              not specified
Symbolic:            r-sr-xrwt
Numeric:             5557
```

## Explain symbolic permissions

```
~/projects/right
[serr@lap]-> ./rights rwsr-sr-t
File type:           not specified
Owner permissions:   read, write, execute with suid (run as file owner)
Group permissions:   read, no write, execute with sgid (run as group member)
Others permissions:  read, no write, sticky bit (for directories: only owner or root can delete files)
Suffix:              not specified
Symbolic:            rwsr-sr-t
Numeric:             7755
```

```
~/projects/right
[serr@lap]-> ./rights crw-rw----+
File type:           character device
Owner permissions:   read, write, no execute
Group permissions:   read, write, no execute
Others permissions:  no read, no write, no execute
Suffix:              ACL present (Access Control Lists)
Symbolic:            crw-rw----+
Numeric:             660
```

## Explain file permissions

```
~/projects/rights
[serr@lap]-> rights /
File type:           directory
Owner permissions:   read, write, execute
Group permissions:   read, no write, execute
Others permissions:  read, no write, execute
Suffix:              not specified
Symbolic:            drwxr-xr-x
Numeric:             755
```

```
~/projects/rights
[serr@lap]-> rights /dev/video0
File type:           character device
Owner permissions:   read, write, no execute
Group permissions:   read, write, no execute
Others permissions:  no read, no write, no execute
Suffix:              ACL present (Access Control Lists)
Symbolic:            crw-rw----+
Numeric:             660
```

# Requirements

- Perl 5.10 or newer (given/when feature)
- `ls` program (optional for most modes, required for file/directory arguments)