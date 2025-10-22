*notice: The author admits that the reader has read all the explanations from the previous levels in order to understand the explanations provided at level X.*

# Level 0 ---> Level 1

The password of the next level can be found in the `/home/$USER` once logged on the remote server.

```bash
    #!/bin/bash

    sshpass -p "bandit0" ssh bandit0@bandit.labs.overthewire.org -p 2220 "grep 'password' *"

```

- `#!/bin/bash` is a 'shebang' that tell the local machine what interpreter to use before executing the script.
- `sshpass` is a command that simulate user interaction on the terminal by injecting the password provided after the `-p` option.
- `ssh` is a command used to connect to remote server by providing the username and domain name separated by '@' of the remote machine. Since the ssh service doesn't run on the default port 22, the -p option tell which port is used. The argument between "" execute the command specified once logged.
- `grep` is a command used to search for a pattern on one or more files.
- `*` is a wildcard that can replace any character or string.

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

    sshpass -p "MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx" ssh bandit3@bandit.labs.overthewire.org -p 2220 "find \$(ls) -type f -iname '.*' -exec cat {} +"
```
- `$()` syntax is used to execute the command between it before passing the output to another command. The escape character is used to avoid the local shell executing the command between it.
- The find command is used to search a file into a specified directory that will be provided by `$(ls)`. The `-type f` flag is used to tell the command to search all file in the specified directory. The `-iname '.*'` and `-exec cat {} +` flag is used respectively to tell the command to search a file with the name begining with `.` and execute the command provided that will print the password of the next level in the shell.

```
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

backend: gibson-0
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ

```

# Level 4 ---> Level 5

The password of the next level can be found in the only human-readable file in the inhere directory.

```bash
    #!/bin/bash
    
    sshpass -p "2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ" ssh bandit4@bandit.labs.overthewire.org -p 2220 "cat \$(find ./inhere -type f -exec file {} + | grep -i ascii | cut -d ':' -f1)"

```
- The file command provided after -exec flag is used to determine the type of file the user deal with.
- `|` is a pipe used to pass the output of the find command to be the input of the grep command.
- The cut command is used to parse the output of a command delimited by `:` and take only the first field. 

```
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

backend: gibson-0
4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
```

# Level 5 ---> Level 6

The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties: human-readable, 1033 bytes in size, not executable

```bash
    #!/bin/bash

    sshpass -p "4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw" ssh bandit5@bandit.labs.overthewire.org -p 2220 "find . -type f -size 1033c -not -executable -exec cat {} +" 
```

- `-size` flag is used to tell the command to search only a file with 1033 bytes.
- `-executable` flag is a flag used to search for all executable file in the specified directory. Since `-not` is provided before it, all files that is not executable is expected as the output.

```
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

backend: gibson-0
HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
``` 

# Level 6 ---> Level 7

The password for the next level is stored somewhere on the server and has all of the following properties: owned by user bandit7, owned by group bandit6, 33 bytes in size.

```bash
    #!/bin/bash


    sshpass -p "HWasnPhtq9AVKe0dmk45nxy20cvUa6EG" ssh bandit6@bandit.labs.overthewire.org -p 2220 "find / -type f -user bandit7 -group bandit6 -size 33c -
exec cat {} + 2> /dev/null"
```

- The `-user` and `-group` option is used respectively to search for all files owned by bandit7 and where the user group is bandit6.
- `2>` is used to redirect all errors like `permission denied` into the black hole `/dev/null`. That means that any errors isn't printed on the screen.

```
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

backend: gibson-0
morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
```

# Level 7 ---> Level 8

The password for the next level is stored in the file data.txt next to the word millionth.

```bash
    #!/bin/bash

    sshpass -p "morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj" ssh bandit7@bandit.labs.overthewire.org -p 2220 "grep millionth data.txt"    
```

```
                             _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

backend: gibson-1
millionth       dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```


