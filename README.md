# rights - Linux file permissions explainer

```
What is it : Linux file permissions explainer
Usage      : rights PERMISSIONS

Arguments:
  PERMISSIONS  File permissions in various formats:
               Symbolic : rwxr-xr-x, rw-------, r-x--x--x
               Numeric  : 755, 644, 777, 600, 444

Examples:
  rights 755        Explain what 755 means
  rights rwxr-xr-x  Explain symbolic permissions
```

# Examples

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

# Requirements

Perl 5.10 or newer (given/when feature)