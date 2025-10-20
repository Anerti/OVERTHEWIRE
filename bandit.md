# Level 0 ---> Level 1

The password of the next level can be found in the `/home/$USER` once logged on the remote server.

```bash
    #!/bin/bash

    sshpass -p "bandit0" ssh bandit0@bandit.labs.overthewire.org -p 2220 "grep 'password' *"

```

- `#!/bin/bash` is a 'shebang' that tell the local machine what interpreter to use before executing the script.
- `sshpass` is a command that simulate user interaction on the terminal by injecting the password provided after the `-p` option.
- `ssh` is a command used to connect to remote server by providing the username and domain name separated by '@' of the remote machine. Since the ssh service doesn't run on the default port 22, the -p option tell which port is used. The argument between "" execute the command specified once logged.

```
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

backend: gibson-1
The password you are looking for is: ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If
```

# Level 1 ---> Level 2

The password of the next level can be found in a file named `-`.

```bash
    #!/bin/bash
    
    sshpass -p "ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If" ssh bandit1@bandit.labs.overthewire.org -p 2220 "cat < -"
    
```
- Since `-` is used to precise the argument of a command, reading a file with name that begin with `-` can be an issue. The `<` is a file descriptor that redirect the standart input to the cat command. Another method is using the relative `./-` or absolute path `/home/$USER/-` of the file.

```                      _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

backend: gibson-1
263JGJPfgU6LtdEvgfWU1XP5yac29mFx
```

# Level 2 ---> Level 3

The password of the next level can be found in a file named `--space in this filename--` in the `/home/$USER` directory.

```bash
    #!/bin/bash

    sshpass -p "263JGJPfgU6LtdEvgfWU1XP5yac29mFx" ssh bandit2@bandit.labs.overthewire.org -p 2220 "cat < '--spaces in this filename--'" 
```
- This level is like the previous level but the filename now contains spaces.To solve this, the filename can be wrapped around `''` or usins escaping characters `--spaces\ in\ this\ filename--`.

```
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

backend: gibson-1
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx

```

# Level 3 ---> Level 4

The password of the next level is in an hidden file in the `/home/$USER` directory.

```bash
    #!/bin/bash

    sshpass -p "MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx" ssh bandit3@bandit.labs.overthewire.org -p 2220 "ls -la inhere/; cat inhere/...Hiding-From-You"
```

- `ls` is a command used to list file on the directory provided. The `-l` option tell ls to provide detailled information about the files or directory found in the specified directory.The `-a` option is used to print all files including those who are hidden. All files hidden begin with `.` .The `.` and `..` directory represent respectively  the current directory and the parent directory.

```                      _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

backend: gibson-1
total 12
drwxr-xr-x 2 root    root    4096 Oct 14 09:26 .
drwxr-xr-x 3 root    root    4096 Oct 14 09:26 ..
-rw-r----- 1 bandit4 bandit3   33 Oct 14 09:26 ...Hiding-From-You
    
```

