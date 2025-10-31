*notice*: 
- The author admits that the reader has read all the explanations from the previous levels in order to understand the explanations provided at level X. The password or the challenge of any level can change anytime*.
- *All script provided below are tested in unix like operating system Ubuntu 24.04.3 LTS. If a command in a script is not found execute* `sudo apt-get update && apt install name_of_the_command` *before executing the script* 
- *To execute any of the script provided below, copy and paste it into a blanck file and give it the right permission before execution it* `chmod +x name_of_the_file.sh && ./name_of_the_file.sh`.



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

# Level 8 ---> Level 9

The password for the next level is stored in the file data.txt and is the only line of text that occurs only once.

```bash
    #!/bin/bash

    sshpass -p "dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc" ssh bandit8@bandit.labs.overthewire.org -p 2220 "cat data.txt | sort | uniq -u"
```

- `sort` command is used to sort alphabetically the output of the previous command `cat`.
- `uniq` can report or omit repeated lines and `-u` option display on the screen uniques lines. `uniq -u` work only if all lines are sorted.

```
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

backend: gibson-1
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```

# Level 9 ---> Level 10

The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.

```bash
    #!/bin/bash

    sshpass -p "4CKMh1JI91bUIZZPXDqGanal4xvAg0JM" ssh bandit9@bandit.labs.overthewire.org -p 2220 "strings data.txt | grep ==="
```

- Unlike `cat`, `strings` command only display human-readable strings. Another alternative is to use `-a` option of `grep` that tells the command to treat binary file as ascii text `grep -a === "data.txt"` but since the output contains binary data, some character is not printable in the terminal and the first option is prefered.

```
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

backend: gibson-1
========== the
========== password
f\Z'========== is
========== FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
```

# Level 10 ---> Level 11

The password for the next level is stored in the file data.txt, which contains base64 encoded data.

```bash
    #!/bin/bash

    sshpass -p "FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey" ssh bandit10@bandit.labs.overthewire.org -p 2220 "base64 -d data.txt"
```

- Base64 encoding is a binary-to-text encoding scheme that converts binary data into an ASCII string format. The `base64` command is a built-in linux command that allow encode/decode data and print to standard output. By default this command encode data provided from input into a basse64 and `-d` option do the reverse operation.

```
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

backend: gibson-1
The password is dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
```

# Level 11 ---> Level 12

The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions.

```bash
    #!/bin/bash

    sshpass -p "dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr" ssh bandit11@bandit.labs.overthewire.org -p 2220 "tr 'a-zA-Z' 'n-za-mN-ZA-M' < data.txt" 
```

- Rotating characters by x positions is called Caesar cipher. The `tr` command allow translating or deleting characters. Here the command is tasking to replace a to n, b to m, c to o ... and the same operation applies to uppercase character from the provided input `data.txt`. But digit remains unchanged.

```
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

backend: gibson-1
The password is 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
```

# Level 12 ---> Level 13

The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed.

```bash
    #!/bin/bash

    sshpass -p "7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4" ssh bandit12@bandit.labs.overthewire.org -p 2220 "DIR=\$(mktemp -d) && cd \$DIR && cp /home/\$USER/data.
txt \$DIR && xxd -r data.txt | gzip -d | bzip2 -d | gzip -d | tar -xvO | tar -xvO | bzip2 -d | tar -xvO | gzip -d"
```

- `mktemp` with `-d` option is used to create a temporary directory. Once created, the name of the temporary directory is stocked in a bash variable `DIR`.
- `&&` is used to chain command only if the first command succeed.
- `cd` is uded to mote to the temporary directory.
- `cp` is a command used to copy a the file `/home/$USER/data.txt` to the temporary directory created previously.
- `xxd` is a command to represent a file to hexadecimal format or make the reverse process with `-r` option.
- `gzip` and `bzip2` are used to compress a file or make the reverse process with `-d` option.
- `tar` is an archive utility used here to extract an archive `-x` directly to the standart output `-O`. The `-v` option tells the command to be verbose.

```
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

backend: gibson-1
data5.bin
data6.bin
data8.bin
The password is FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn
```

# Level 13 ---> Level 14

In this level, an ssh private key is provided in `\home\$USER` to loggin in the next level instead of using a password.

```bash
    #!/bin/bash

    sshpass -p "FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn" scp -P 2220 bandit13@bandit.labs.overthewire.org:/home/bandit13/sshkey.private /home/$USER && cat /home/$USER/sshkey.private && echo -e "\nPrivate key downloaded to /home/$USER/\n"
```

- `scp` stand for secure copy that permit to download a file based on his absolute path from remote machine to the local machine. Since ssh doesn't run on the default port 22, `-P` option specify the port.
- `echo` display a line of text and the `-e` option enable the interpretation of backslash.

```
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

backend: gibson-1
-----BEGIN RSA PRIVATE KEY-----
MIIEpAIBAAKCAQEAxkkOE83W2cOT7IWhFc9aPaaQmQDdgzuXCv+ppZHa++buSkN+
gg0tcr7Fw8NLGa5+Uzec2rEg0WmeevB13AIoYp0MZyETq46t+jk9puNwZwIt9XgB
ZufGtZEwWbFWw/vVLNwOXBe4UWStGRWzgPpEeSv5Tb1VjLZIBdGphTIK22Amz6Zb
ThMsiMnyJafEwJ/T8PQO3myS91vUHEuoOMAzoUID4kN0MEZ3+XahyK0HJVq68KsV
ObefXG1vvA3GAJ29kxJaqvRfgYnqZryWN7w3CHjNU4c/2Jkp+n8L0SnxaNA+WYA7
jiPyTF0is8uzMlYQ4l1Lzh/8/MpvhCQF8r22dwIDAQABAoIBAQC6dWBjhyEOzjeA
J3j/RWmap9M5zfJ/wb2bfidNpwbB8rsJ4sZIDZQ7XuIh4LfygoAQSS+bBw3RXvzE
pvJt3SmU8hIDuLsCjL1VnBY5pY7Bju8g8aR/3FyjyNAqx/TLfzlLYfOu7i9Jet67
xAh0tONG/u8FB5I3LAI2Vp6OviwvdWeC4nOxCthldpuPKNLA8rmMMVRTKQ+7T2VS
nXmwYckKUcUgzoVSpiNZaS0zUDypdpy2+tRH3MQa5kqN1YKjvF8RC47woOYCktsD
o3FFpGNFec9Taa3Msy+DfQQhHKZFKIL3bJDONtmrVvtYK40/yeU4aZ/HA2DQzwhe
ol1AfiEhAoGBAOnVjosBkm7sblK+n4IEwPxs8sOmhPnTDUy5WGrpSCrXOmsVIBUf
laL3ZGLx3xCIwtCnEucB9DvN2HZkupc/h6hTKUYLqXuyLD8njTrbRhLgbC9QrKrS
M1F2fSTxVqPtZDlDMwjNR04xHA/fKh8bXXyTMqOHNJTHHNhbh3McdURjAoGBANkU
1hqfnw7+aXncJ9bjysr1ZWbqOE5Nd8AFgfwaKuGTTVX2NsUQnCMWdOp+wFak40JH
PKWkJNdBG+ex0H9JNQsTK3X5PBMAS8AfX0GrKeuwKWA6erytVTqjOfLYcdp5+z9s
8DtVCxDuVsM+i4X8UqIGOlvGbtKEVokHPFXP1q/dAoGAcHg5YX7WEehCgCYTzpO+
xysX8ScM2qS6xuZ3MqUWAxUWkh7NGZvhe0sGy9iOdANzwKw7mUUFViaCMR/t54W1
GC83sOs3D7n5Mj8x3NdO8xFit7dT9a245TvaoYQ7KgmqpSg/ScKCw4c3eiLava+J
3btnJeSIU+8ZXq9XjPRpKwUCgYA7z6LiOQKxNeXH3qHXcnHok855maUj5fJNpPbY
iDkyZ8ySF8GlcFsky8Yw6fWCqfG3zDrohJ5l9JmEsBh7SadkwsZhvecQcS9t4vby
9/8X4jS0P8ibfcKS4nBP+dT81kkkg5Z5MohXBORA7VWx+ACohcDEkprsQ+w32xeD
qT1EvQKBgQDKm8ws2ByvSUVs9GjTilCajFqLJ0eVYzRPaY6f++Gv/UVfAPV4c+S0
kAWpXbv5tbkkzbS0eaLPTKgLzavXtQoTtKwrjpolHKIHUz6Wu+n4abfAIRFubOdN
/+aLoRQ0yBDRbdXMsZN/jvY44eM+xRLdRVyMmdPtP8belRi2E2aEzA==
-----END RSA PRIVATE KEY-----

Private key downloaded to /home/anerti/
```

# Level 14 ---> Level 15

The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.

*notice: This level depends on the previous level because the sshkey.private file need to be downloaded to /home/$USER*

```bash
    #!/bin/bash

    chmod 600 /home/$USER/sshkey.private && ssh bandit14@bandit.labs.overthewire.org -p 2220 -i /home/$USER/sshkey.private "nc -v localhost 30000 < /etc/bandit_pass/\$USER"
```

- `chmod` change the file permission to set read and write permission for the owner (`600`) of the file provided. If the permission is not correctly set, An issue will occurs during the ssh connection.
- The `-i` option tell ssh to use the private key provided instead of using a password to login
- `nc` enable UDP or TCP connection to a machine in the same network. `-v` option tell the command to make verbose output, the `localhost` or `127.0.0.1` is the ip address of a local machine and 30000 is the port in which to connect. Once the connection is established, the file located in `/etc/bandit_pass/$USER` will be sent. Another alternative is to use `telnet`.

```                      _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

backend: gibson-1
Connection to localhost (127.0.0.1) 30000 port [tcp/*] succeeded!
Correct!
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
```

# Level 15 ---> Level 16

The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL/TLS encryption.

```bash
    #!/bin/bash

    sshpass -p "8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo" ssh bandit15@bandit.labs.overthewire.org -p 2220 "ncat --ssl localhost 30001 <<< 8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo"     
```

- `ncat` is like `nc` but the communication can be encrypted with ssl by using `--ssl` option to communicate to https server according to the [Official documentation](https://nmap.org/ncat/guide/ncat-ssl.html). 
- Another method is using `openssl` to submit the password over ssl/tls encrypted communication `openssl s_client localhost:30001`. According to the man page `s_client` option implements a generic SSL/TLS client which can establish a transparent connection to a remote server speaking SSL/TLS. Once the connection is established, the password must be submited manually. 

```
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

backend: gibson-1
Correct!
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
```

# Level 16 ---> Level 17

The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000.

```bash
    #!/bin/bash

    sshpass -p "kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx" ssh bandit16@bandit.labs.overthewire.org -p 2220 "DIR=\$(mktemp -d) && nmap localhost -p 31000-32000 -oG \$DIR/target && for port in \$(grep -oE '[0-9]{5}' \$DIR/target); do ncat --ssl localhost \$port <<< 'kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx'; done" 
```

- nmap (Network Mapper) is a tool commonly used to discover hosts and scan their ports. In this script, `localhost` is the target, and `-p 31000‑32000` specifies the range of ports to scan. The `-oG` option tells `nmap` to save the results in a greppable format to `$DIR/target`.
- The loop `for port in $PORTS; do COMMAND; done` repeats a command for each port found by the scan. The ports are extracted from the greppable output using `grep -oE '[0-9]{5}'`, which matches five‑digit numbers. For each extracted port, the command `ncat --ssl localhost $port <<< 'kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx'` is executed, sending the password over an SSL‑encrypted connection.
- Another method to scan ports between 31000 and 32000 is to use `nc -zv localhost 31000‑32000 2>&1 | grep succeeded` instead of `nmap`. The `-z` option tells Netcat to scan the ports, and `2>&1` redirects all error output to stdout so that it makes it possible to filter the successful connections with `grep`.


```
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

backend: gibson-1
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-10-27 15:59 UTC
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00020s latency).
Not shown: 996 closed tcp ports (conn-refused)
PORT      STATE SERVICE
31046/tcp open  unknown
31518/tcp open  unknown
31691/tcp open  unknown
31790/tcp open  unknown
31960/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 0.11 seconds
Ncat: Connection refused.
Ncat: Connection refused.
Ncat: Input/output error.
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
Ncat: Input/output error.
Correct!
-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ
imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ
Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu
DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW
JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX
x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD
KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl
J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd
d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC
YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A
vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama
+TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT
8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx
SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd
HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt
SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A
R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi
Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg
R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu
L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni
blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU
YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM
77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b
dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3
vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=
-----END RSA PRIVATE KEY-----

Ncat: Input/output error.
```

# Level 17 ---> Level 18

The password for the next level is in passwords.new and is the only line that has been changed between passwords.old and passwords.new in the /home/$USER directory.

```bash
#!/bin/bash

echo "-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ
imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ
Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu
DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW
JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX
x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD
KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl
J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd
d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC
YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A
vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama
+TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT
8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx
SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd
HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt
SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A
R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi
Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg
R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu
L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni
blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU
YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM
77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b
dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3
vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=
-----END RSA PRIVATE KEY-----" > /tmp/sshprivatekey && chmod 600 /tmp/sshprivatekey && ssh -i /tmp/sshprivatekey bandit17@bandit.labs.overthewire.org -p 2220 "diff passwords.new passwords.old"    
```

- `diff` is a command used to compare files line by line.

```
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

backend: gibson-1
42c42
< x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
---
> pGozC8kOHLkBMOaL0ICPvLV1IjQ5F1VA
```

# Level 18 ---> Level 19

The password for the next level is stored in a file readme in the homedirectory. Unfortunately, someone has modified .bashrc to log in out when logged in with SSH.

```bash
    #!/bin/bash

    sshpass -p "x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO" ssh bandit18@bandit.labs.overthewire.org -p 2220 "cat readme"
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
cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8
```

# Level 19 --> Level 20

The password for this level can be found in the usual place (/etc/bandit_pass), after the setuid binary has been used.

```bash
    #!/bin/bash

    sshpass -p "cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8" ssh bandit19@bandit.labs.overthewire.org -p 2220 "ls -l bandit20-do; ./bandit20-do cat /etc/bandit_pass/bandit20
```
- A setuid binary is a file that will always execute with the privileges of its owner.

```
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

backend: gibson-1
-rwsr-x--- 1 bandit20 bandit19 14884 Oct 14 09:26 bandit20-do
0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
```

# Level 20 ---> Level 21

There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).

*Notice: This level require 2 terminal*

```bash
    #!bin/bash

    sshpass -p "0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO" ssh bandit20@bandit.labs.overthewire.org -p 2220 "nc -lvnp 4444 <<< 0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO"
```
- On the first terminal, run the script above to start Netcat. The `-l` option makes Netcat listen on the specified port `-p` 4444, which binds to all interfaces by default, and the `-n` option disables DNS resolution to speed up the process. 
- The <<< operator sends the specified password.


```bash
    #!/bin/bash

    sshpass -p "0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO" ssh bandit20@bandit.labs.overthewire.org -p 2220 "./suconnect 4444"
```
- Once a notification `Listening on 0.0.0.0 4444` appears in the first terminal, run the script above that connects to that terminal. 
- The suconnect program is a set‑uid binary that likely looks something like this: `nc localhost $PORT <<< "password"`.

In short, this establishes a reverse shell: the remote machine waits for an incoming connection, and the target machine executes a script that connects back to the remote host.


```
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

backend: gibson-1
Listening on 0.0.0.0 4444
EeoULMCra2q0dSkYj561DX7s1CpBuOBt
Connection received on 127.0.0.1 54300
```

# Level 21 ---> Level 22

A program is running automatically at regular intervals from cron, the time-based job scheduler.

```bash
    #!/bin/bash


    sshpass -p "EeoULMCra2q0dSkYj561DX7s1CpBuOBt" ssh bandit21@bandit.labs.overthewire.org -p 2220 "find /etc/cron.d/ -type f -readable -exec cat {} +; echo -e '\n\n'; cat /usr/bin/cronjob_bandit22.sh; echo -en '\n\nThe password of the next level is: '; cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv"
```

- The `-readable` option in `find` matches files that are readable by the current user (bandit21 in this case) and displays them using `-exec`.
- The /etc/cron.d directory holds all additional configuration files for the cron daemon to schedule tasks.
- Since `/usr/bin/cronjob_bandit22.sh` looks interesting, its contents reveal that a copy of the next‑level password is stored in the file `/tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv`.


```
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

backend: gibson-1
@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
@reboot bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
* * * * * bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
30 3 * * 0 root test -e /run/systemd/system || SERVICE_MODE=1 /usr/lib/x86_64-linux-gnu/e2fsprogs/e2scrub_all_cron
10 3 * * * root test -e /run/systemd/system || SERVICE_MODE=1 /sbin/e2scrub_all -A -r
# DO NOT EDIT OR REMOVE
# This file is a simple placeholder to keep dpkg from removing this directory
# The first element of the path is a directory where the debian-sa1
# script is located
PATH=/usr/lib/sysstat:/usr/sbin:/usr/sbin:/usr/bin:/sbin:/bin

# Activity reports every 10 minutes everyday
5-55/10 * * * * root command -v debian-sa1 > /dev/null && debian-sa1 1 1

# Additional run at 23:59 to rotate the statistics file
59 23 * * * root command -v debian-sa1 > /dev/null && debian-sa1 60 2
@reboot bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
* * * * * bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
*/30 * * * * root find /tmp -amin 60 -type f -delete &> /dev/null && find /tmp -amin 5 -type d -empty -delete &> /dev/null



#!/bin/bash
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv


The password of the next level is: tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q
```

# Level 22 ---> Level 23

A program is running automatically at regular intervals from cron, the time-based job scheduler.

```bash
    #!/bin/bash

    sshpass -p "tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q" ssh bandit22@bandit.labs.overthewire.org -p 2220 "find /etc/cron.d/ -type f -readable -exec cat {} +; echo -e '\n\ncontent of the /usr/bin/cronjob_bandit23.sh script:\n'; cat /usr/bin/cronjob_bandit23.sh; echo -en '\n\nThe password of the next level is: '; cat /tmp/\$(echo I am user bandit23 | md5sum | cut -d ' ' -f 1)"

```

- Since the contents of `/usr/bin/cronjob_bandit23.sh` look interesting, the script reveals that the scheduled task computes the MD5 checksum of the current username (bandit22  in this case) and creates a copy of the next‑level password in /tmp. The copy is named with the MD5 hash of the username.


```
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

backend: gibson-1
@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
@reboot bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
* * * * * bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
30 3 * * 0 root test -e /run/systemd/system || SERVICE_MODE=1 /usr/lib/x86_64-linux-gnu/e2fsprogs/e2scrub_all_cron
10 3 * * * root test -e /run/systemd/system || SERVICE_MODE=1 /sbin/e2scrub_all -A -r
# DO NOT EDIT OR REMOVE
# This file is a simple placeholder to keep dpkg from removing this directory
# The first element of the path is a directory where the debian-sa1
# script is located
PATH=/usr/lib/sysstat:/usr/sbin:/usr/sbin:/usr/bin:/sbin:/bin

# Activity reports every 10 minutes everyday
5-55/10 * * * * root command -v debian-sa1 > /dev/null && debian-sa1 1 1

# Additional run at 23:59 to rotate the statistics file
59 23 * * * root command -v debian-sa1 > /dev/null && debian-sa1 60 2
@reboot bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
* * * * * bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
*/30 * * * * root find /tmp -amin 60 -type f -delete &> /dev/null && find /tmp -amin 5 -type d -empty -delete &> /dev/null


content of the /usr/bin/cronjob_bandit23.sh script:

#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget


The password of the next level is: 0Zf11ioIjMVN551jX3CmStKLYqjk54Ga
```

# Level 23 ---> Level 24

A program is running automatically at regular intervals from cron, the time-based job scheduler.

```bash
    #!/bin/bash

    #script issues 
```

# Level 24 ---> Level 25

A daemon is listening on port 30002 and will give you the password for bandit25 if given the password for bandit24 and a secret numeric 4-digit pincode.

```bash
    #!/bin/bash

    sshpass -p "gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8" ssh bandit24@bandit.labs.overthewire.org -p 2220
```

- Once logged in, execute `cd $(mktemp -d)`, copy the script provided below, create a file with vi `filename.py`, and paste the script into it. 
- Give it execute permission with `chmod +x filename.py` and run it with `./filename.py`. 

Depending on how long the PIN is, it may take some time to find the correct PIN.

This time, a Python script will be used to automate the program's interactions by using pwntools.

```python
    #!/usr/bin/python3
    from pwn import *


    p = remote('127.0.0.1', 30002)

    for number in range(0, 9999):
        code = "gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8"
        if number < 10:
            code += f" 000{number}"
        elif (number >= 10 and number < 100):
            code += f" 00{number}"
        elif (number >= 100 and number < 1000):
            code += f" 0{number}"
        else:
            code += f" {number}"

        print(f"Trying {code} ...")
        p.writeline(code.encode('latin-1'))
        checker = p.clean(0.2).decode('latin-1').split(" ")

        if checker != 'Wrong!' or checker != 'I':
            break
```
- The function `remote(IP_ADRESS, PORT)` is used to connect to the given address and port. 
- `p.writeline(code.encode('latin-1'))` sends the given string as bytes.
- `p.clean(0.2)` receives the output.

The program will run until the password is found from 0000 to 9999.

```
PIN code found gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8 1667
[*] Closed connection to 127.0.0.1 port 30002
```
- When the password is found log out and execute the script below retrieve the password of the next level.

```bash
    #!/bin/bash

    sshpass -p "gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8" ssh bandit24@bandit.labs.overthewire.org -p 2220 "nc -vn 127.0.0.1 30002 <<< 'gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8 1667'"
```

```                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

backend: gibson-1
I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.
Correct!
The password of user bandit25 is iCi86ttT4KSNe1armKiwbQNmB3YJP3q4

Connection to 127.0.0.1 30002 port [tcp/*] succeeded!
```
