## File and directory permissions

Setting permissions on file and directories is important in the linux system. This makes it to manager access to certain files in the system based on groups and users. This permissions can be set on files and directories.

#### Sets of permissions
There are three types of permissions  groups that can me set on file and directories in linux systems. They include:

  - `r` Read.
  - `w` Write.
  - `x` Execute.
  - `-` None

permissions start with either `-` or `d`. This specifies whether these are file or directory permissions and `-` for file permissions.
```
drwxrwxr-x: directory permissions

-r-xrwxr--: file permissions

 ```
 permissions are set following this format `user->group->others`. Using the example above
 ```
 -r-xrwxr--: user = r-x, group=rwx and others r--
```
 This means that the user can only read and execute, while the group can read, write and execute  while others can only read.


permissions groups can also be denoted using octed notation

  - `4` Read.
  - `2` Write.
  - `1` Execute.
  - `0` None

  ```
  -r-xrwxr = (4+0+1)(4+2+1)(4+0+0)

  The final octed permissions will be 574

  ```
