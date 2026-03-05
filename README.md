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