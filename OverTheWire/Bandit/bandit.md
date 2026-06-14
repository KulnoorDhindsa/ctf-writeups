# Level 0 → 1
### Objective:  Find the password for level 1 stored in a file readme located in the home directory.
### What I thought and executed:
1. I ran `man` on the suggested commands (`ls`, `du`, `cat`, `file`, `cd`(no `man cd` exists) and `find`) in the official site for overthewire bandit i.e. [OverTheWire Bandit](https://overthewire.org/wargames/bandit/).
2. `ls` lists all the files readable/nonreadable present in the current directory.
3. `cat` reads the content of a selected file and displays output in the terminal .
### What was required:
| Command Required (in order)   | Purpose                                                      |
|-------------------------------|--------------------------------------------------------------|
|`ls`                           | To confirm that a file 'readme' exists in the directory.     |
|`cat readme`                   | To read the file 'readme' for readable content               |
### What I learnt:
- SSH sessions start in the user's home directory by default.
- In `bandit1@bandit.labs.overthewire.org -p 2220`, *bandit1* is the username, *bandit.labs.overthewire* is the server address and *-p 2220* is the port address.

---

# Level 1 → 2
### Objective: Find the password for level 2 stored in a file '-' located in the home directory.
### What I thought and executed:
1. To confirm that a file '-' exists in the home directory, I ran `ls`, and surely it was there.
2. To read its contents I ran `cat -`. This froze my terminal.
3. I read in the 'Helpful Reading Material' section on [OverTheWire Bandit](https://overthewire.org/wargames/bandit/), that files beginning with '-' pose a problem to a few Linux commands, including `cat`. The correct way to run `cat` on these file names is `cat ./filename`.
### What was required:
|Command Required (in order)  | Purpose                                                |
|-----------------------------|--------------------------------------------------------|
|`ls`                         |To confirm that a file '-' exists in the home directory |
|`cat ./-`                    |To read the file '-' for the password                   |
### What I learnt:
- `cat -` freezes the terminal as `-` is a Unix convention for stdin (standard input), so `cat -` waits for keyboard input, causing the terminal to freeze.
- '-' poses a problem for a few Linux commands. `cat ./-` works (where '.' is for current directory, '/' is a separator. `./`) as it tells shell to interpret `-` as a **path** rather than a flag/option.

---

# Level 2 → 3
### Objective: Find the password for level 3 stored in a file 'spaces in this filename' located in the home directory.
### What I thought and executed:
1. I ran `ls` command to confirm that a file 'spaces in this filename' exists in this directory.
2. I ran `cat ./spaces in this filename`. This failed as it took 'spaces', 'in', 'this' and 'filename' as different filenames which obviously didn't exist in the home directory.
3. I read the 'Helpful Reading Material' section on the [OverTheWire Bandit](https://overthewire.org/wargames/bandit/) for this particular level. 
4. I found two solutions:
    - Instead of `cat ./spaces in this filename`, I ran `cat ./spaces\ in\ this\ filename` which tells the shell to treat the soace following `\` as part of the filename rather than a separator.
    - *shortcut* : Press tab after './spaces'. The system automatically types the file matching this initial name with the required additions of '\' wherever required. However this method fails when there are multiple files with the same prefix.
### What was required:
| Commands Required (in order)            |Purpose                                                                                       |
|-----------------------------------------|----------------------------------------------------------------------------------------------|
|`ls`                                     |To confirm that a file 'readme' exists in the home directory                                  |
|`cat ./spaces\ in\ this\ filename` |To read the content of the file 'spaces in this filename' appropriately for the password|
### What I learnt:
- Shell by default interprets spaces as arguments and `-` as flag prefix. Thus while writing filenames, *spaces* and `-` are followed by `\`. 
- '\' is used to let the system know that the following space is to be used as a charcters rather than a separator. 

---

# Level 3 → 4
### Objective: Find the password for level 4 stored in a hidden file in the 'inhere' directory
### What I thought and executed:
1. The `find` command is used to search for files and directories on the server.
2. I ran the command `find [inhere]` - *incorrect syntax, brackets are not used.* Simply `find inhere` works.
3. I ran `ls` in my home directory in hopes that it will read content of all the directories, which was a rookie mistake. Since `man cd` didnt exist, it took me some googling to realise that `cd` command is used to change directories.
4. I ran `file inhere` to confirm that its a directory (it showed 'inhere' in blue).
5. I ran `cd inhere` followed by `ls` in the inhere directory. No results for `ls` as it was a hidden file.
6. I ran `ls -a` in the inhere directory, as this command lists all hidden files aswell.
7. Hidden files in Linux are just files that begin with fullstop (.).
8. Then I ran `cat` for the hidden file to read its content.
### What was required:
|Commands Required (in order)|Purpose                                             |
|----------------------------|----------------------------------------------------|
|`cd inhere`                 |To switch from home directory to 'inhere' directory |
|`ls -a`                     |To list hidden files in the directory               |
|`cat filename`              |To read the content of the file                     |
### What I learnt:
- While using `file` command, no need to use [] for the filename, its the wrong syntax, instead `file filename` is correct.
- `ls` can list readable directory entries.
- By default in most terminals, `ls` color-codes output, with **directories typically shown in blue**.
- `ls -a` can list hidden files.
- Hidden files are just files that begin with full stop (.).

---

# Level 4 → 5
### Objective: Find the password for level 5 stored in human-readable file in the 'inhere' directory
### What I thought and executed: 
1. I ran `cd inhere`.
2. There were a number of files. There are 2 options:
    - I run `file` command on all individual files untill i get *ASCII* file, which is the human readable file. This method works but is long isn't that efficient when dealing with large amount of files.
    - I run `file ./*`. This command files or categorises each file type in the current directory. '.' for this directory, '/' as a separator and '*' for everything.
### What was required:
|Commands Required (in order)|Purpose                                                            |
|----------------------------|-------------------------------------------------------------------|
|`cd inhere`                 |To switch directories to 'inhere' from home directory              |
|`file ./*`                  |To check file types of all files in the current 'inhere' directory |
|`cat filename`              |To read the filename for the password                              |
### What I learnt: 
- `*` is a *glob/wildcard* that the shell expnds to all filenames in the current directory.
- `./*` expands to all files in current directory, passing them as arguments to the command.

---

# Level 5 → 6
### Objective: To find the password for level 6 stored in a directory in 'inhere' directory with '1033 byte size', 'not executable' and 'human readable'.
### What I thought and executed:
1. I ran `cd inhere` to switch directories.
2. I ran `file ./*` and got 19 'maybehere' directories.
3. Now we need a directory that is human readable (ASCII text), file size 1033 bytes (`du` command can help) and non executable.
4. We can `cd` into every directory one by one which is a long and tedious task.
5. I ran `man find` to figure out how to use specifications like size. After `man find`, you can type '/size' to find the keyword 'size' in the entire manual page.
6. For the 'non-executabele' file ( a file that can't be run as a programme in itself) using `! -executable` works.
7. I finally ran `find . -size 1033c ! -executable` where, '.' to find in the current directory ('inhere'), '-' used for different criterias applied (like size), 'c' to specify bytes and '!' for 'non'.
### What was required:
|Commands Required (in order)       | Purpose                                                        |
|-----------------------------------|----------------------------------------------------------------|
|`cd inhere`                        |To switch directories from home directory to 'inhere' directory |
|`find . -size 1033c ! -executable` |To find a file of size 1033 bytes and non executable       |
|`cd maybehere07`                   | To switch to desired directory                                 |
|`file ./*`                         |To check the human readable file (ASCII plain text)             |
|`cat file2`                        |To read the desired file for the required password              |
### What I learnt:
- Many further criteria like 'size' 'executable' etc can be applied to `find` command where `-` is a **flag prefix** for each individual option.
- '/word' can be type in the manual page of the `man` command to search for keywords regarding chosen command.
- '!' is for negating commands like 'non executable files'.

---

# Level 6 → 7
### Objective: Find the password for level 7 stored in a file somewhere on the server having properties- owned by owner 'bandit7', group 'bandit6' and '33 byte' in size
### What I thought and executed:
1. I ran `man find` and searched '/user' and '/group' to figure out how to include these specifications in the find.
2. I ran `find / -size 33c -group bandit6 -user bandit7` where '/' searches the entire server, '-' separates the criterias, '33c' is for 33 bytes ('c' in Linux is for bytes).
3. `find /` will return many **permission denied** errors for directories that user *bandit6* can't access.
### What was required:
|Commands Required (in order)                   | Purpose                                  |
|-----------------------------------------------|------------------------------------------|
| `find /-size 33c -group bandit6 -user bandit7` |To find the file with these specifications|
|`cat ./filename`                               |To read the desired file for the password.|
### What I learnt:
- '/' is the **root of the filesystem**. `find /` searches from the root directory downward, covering the entire filesystem.
- '.' searches the current directory.
-  Using '/' in the `man` pages of command allows you to search specific keywords.

---

# Level 7 → 8
### Objective: Find the password for level 8 stored in a file 'data.txt' next to the word 'millionth'
### What I thought and executed:
1. I ran `man` on suggested commands (`man`, `grep`, `sort`, `uniq`, `strings`, `base64`, `tr`, `gzip`, `bzip2` and `xxd`) to find a command that searches based off of patterns or keywords.
2. I ran `grep millionth data.txt`.
3. I got the result and the password was right next to 'millionth'.
### What was required:
|Commands Required (in order)        |Purpose                                                   |
|------------------------------------|----------------------------------------------------------|
|`grep millionth data.txt`           |To search for the word 'millionth' in the file 'data.txt' |
### What I learnt:
- Running `man` command on the suggested commands of that level on [OverTheWire Bandit](https://overthewire.org/wargames/bandit/) helps learning in the long run as we get used to reading large amount of data which is necessary in the security field.
- `grep` command is used to search for patterns (regular expressions) in files.

---

# Level 8 → 9
### Objective: Find the password for level 9 stored in a file 'data.txt' and is the only line of text that appears once
### What I thought and executed:
1. I ran `man` command on the suggested commands of this level, `sort` and `uniq` were to be used but I didnt know how they are used together.
2. I read the page linked under the 'Helpful Reading Material' for 'Pipelines and Redirections' and learnt that '|' is used for pipelining.
3. Pipelining refers to the process where the output for the first command is used as input for the second command.
4. I ran `sort data.txt | uniq -u` where 'sort data.txt' sorts the data based on occurence, '|' is used for pipelining result of `sort data.txt` into `uniq -u` command, `uniq` is command that searches patterns and '-u- is for 'repeated once'.
### What was required:
|Commands Required (in order)        | Purpose                                                               |
|------------------------------------|-----------------------------------------------------------------------|
|`sort data.txt \| uniq -u`           |To sort the file 'data.txt and search for the line repeated only once. |
### What I learnt:
- '|' is the pipeline operator that send the output of the first command into the input of the second command.

---

# Level 9 → 10
### Objective: Find the password for level 10 stored in a file 'data.txt' in few human-readable strings preceded by a number of '=' signs
### What I thought and executed:
1. 'Human-readable strings' refers to texts that are not in binary language or other non-human readable language.
2. Its figured that the `strings` command will be used to sort out the strings in the file data.txt and the `grep` command for searching multiple '===' characters.
3. There are 2 methods now:
    - `strings data.txt` and then manually read the strings, find out the ones that have "===" at the start and read the password from the large output.
    - `strings data.txt | grep "==="` which is a faster and more efficient way when dealing with large amount of files.
4. Pipeline '|' will be used again to feed the output of the `strings` command as the input of the `grep` command.
5. I ran `strings data.txt | grep "==="`.
### What was required :
|Commands required (in order)    |Purpose                                                               |
|--------------------------------|----------------------------------------------------------------------|
|`strings data.txt \| grep "==="` |To search for specific string in data.txt with repeated "===" pattern |
### What I learnt:
- There are surely some combinations of commands that will reduce your required effort to a minimum.

---

# Level 10 → 11
### Objective: Find the password for level 11 stored in the file 'data.txt' containing 'base64' encoded data.
### What I thought and executed:
1. Since I ran `man` command on the suggested commands in the previous levels, and the suggested commands for this level are the same, I knew that `base64` command was to be used.
2. I ran `base64 data.txt` which was the wrong move as this command is for encoding the data, and the data in 'data.txt' is already encoded using 'base64' so it took me some time to figure out the command for decoding the data.
3. I ran `base64 -d data.txt` which decodes the file thus giving me the password for the next level.
### What was required:
|Commands required (in order) | Purpose                                        |
|-----------------------------|------------------------------------------------|
| `base64 -d data.txt`        |To decode the data coded in the file 'data.txt' |
### What I learnt:
- '-d' is for 'decoding' and using command without '-d' is for encoding the selected file further.

---

# Level 11 → 12
### Objective: Find the password for level 12 stored in file 'data.txt' where all lowercase letters (a-z) and uppercase letters (A-Z) have been rotated by 13 postions.
### What I thought and executed:
1. I had very little idea of what the objective meant, thus I went to the 'helpful reading material' 'Rot13' on wikipedia.
2. I found that 'rot13' is a famous patterns used in the past which rotated the selected character in (a-z) and (A-Z) by 13 letters in the forward direction.
3. I figured you have to `cat` this file and then rotate the letters by 13, thus use the `tr` command used to 'translate, delete and squeeze letters' which may mean that it alters the order of the characters.
4. This was the first level where I had no idea of the syntax and googled it. You pipeline from `cat` to `tr` to do rot13.
5. I ran `cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'` where `cat` reads the file 'data.txt', this output then is given to `tr` as the input. `tr` rotates 'A-Za-z' ( A-Z and a-z) to 'N-ZA_Mn-za-m' (Z replaced by N, A replaced by M, n to z and a to m).
### What was required:
|Commands Required (in order)                 |Purpose                                                      |
|---------------------------------------------|-------------------------------------------------------------|
|`ls`                                         |To make sure file 'data.txt' exists in home directory        |
|`cat data.txt \| tr 'A-Za-z' 'N-ZA-Mn-za-m'` |To rotate the characters of file 'data.txt' by 13 characters |
### What I learnt:
- 

---

# Level 12 → 13
### Objective: Find the password for level 13 in a file 'data.txt' which is a hexdump of files repeatedly compressed.
### What I thought and executed:
1. On the official site: [OverTheWire Bandit](https://overthewire.org/wargames/bandit/), it is suggested to make temporary directory and work there so as to not damage the file and read the `man` pages of the suggestsed files I didn't already know (`mkdir`, `cp`, `mv`).
2. I ran `mktemp -d` which makes a temporary directory in which I can work and decompress a copy of the file 'data.txt/ without harming the actual file.
3. Then it gives you an address of the directory (in my case: /tmp/tmp.BlJKXiMlnx).
4. Then I ran `cp ~/data.txt /tmp/tmp.BlJKXiMlnx` to copy the file 'data.txt' to the temporary directory I made earlier.
5. Then I ran `cd /tmp/tmp.BlJKXiMlnx` to switch the temporary directory from the home directory.
6. I ran `ls` to confirm if the file 'data.txt' had been copied or not.
7. I ran `xxd -r data.txt > data` , to reverse the hexdump on the file 'data.txt' to a new file 'data' which is the smae file but with reverse the hexdump.
8. I ran `ls` to see the file 'data' and `file data` to see how it has been compressed.
9. It was gzip compressed. To decompress it, I needed the file to have the extension 'gz', so I used `mv data data.gz` that renamed the file 'data' with the extension 'data.gz'.
10. `mv` command mainly work with the syntax `mv [options] source destination`, if the destination doesnt exist (or left blank), then the file is renamed.
11. I ran `gzip -d data.gz` to decompress the file 'data.gz' where '-d' is for decompress.
12. I ran `file data` to check which compression is on the file now (as the instructions on [OverTheWire Bandit](https://overthewire.org/wargames/bandit/) mention that the file has been *repeatedly* compressed, thus will need multiple decompressions including `tar`, `gzip` and `bzip2`)
13. It was bzip2 compressed. Thus the name of the file data had to change to 'data.bz2' (with the 'bz2' extension for decompression). I ran `mv data data.bz2` followed by `bazip2 -d data.bz2` to decompress ('-d') the file data. I ran `file data` again to see the next decompression to be made. These steps had to be repeatedly followed until the file type shows *ASCII* that is plain text that can be read by humans.
14. It was a 'gzip' compression again so same steps had to be followed. After runing `file` on the newly decompressed file, it was `tar` compressed which has few different steps.
15. This is because unlike 'gzip' or 'bzip2' that compress singular files, 'tar' bundles multiple files into 1 archive (like a zip folder), so after decompression, `ls` also has to be run to check which all files have bin decompressed.
16. I ran `mv data data.tar` and `tar -xf data.tar` to decompress teh files. Here, in '-xf' the '-x' is for *extract*, telling the system to extract the files from the archive and load them to my system. The 'f' is for specifying the archive name that is to be extracted.
17. I ran `ls` and got the file 'data5.bin'. Then `file data5.bin` to find a further 'tar' compression on it. I decompressed it, ran ls on data5.tar, to get a file 'data6.bin' which was gzip compressed, same steps for decompression of gzip followed.
18. On decompression of 'data6.bin' I obtained 'data8.bin' which was gzip compressed, on its decompression, `file data8`, this was an *ASCII* file. I ran `cat data8` and obtained the password for the next level.
### What was required:
|Commands Required (in order)       |Purpose                                                                                  |
|-----------------------------------|-----------------------------------------------------------------------------------------|
|`mktemp -d`                        |To make a unique directory                                                               |
|`cp ~/data.txt /tmp/tmp.BlJKXiMlnx`|To copy teh file 'data.txt' into newly made directory of the address '/tmp/tmp.BlJKZiMlnx|
|`cd /tmp/tmp.BlJKXiMlnx`           |To switch directories                                                                    |
|`xxd -r data.txt > data`           |To reverse the hexdump on 'data.txt' to a  new file 'data'                               |
|`file data`                        |To check the type of compression on 'data'                                               |
|`mv data data.gz`                  |To rename the file 'data' to 'data.gz' to decompress the gzip compression                |
|`gzip -d data.gz`                  |To decompress the file 'data.gz'                                                         |
|`file data`                        |To check the next decompression on file 'data'                                           |
|`mv data data.bz2`                 |To rename the file 'data' to 'data.bz2' to decompress the bzip2 compression              |
|`bzip2 -d data.bz2`                |To decompress the file 'data.bz2'                                                        |
|`file data`                        |To check the next decopression                                                           |
|`mv data data.gz`                  |To rename the file 'data' to 'data.gz' to decompress the 2nd gzip compression            |
|`gzip -d data.gz`                  |To decompress the file 'data.gz'                                                         |
|`file data`                        |To check the next decompression on file 'data'                                           |
|`mv data data.tar`                 |To rename the file 'data' to 'data.tar' to decompress the tar compression                |
|`tar -xf data data.tar`            |To decompress the archive data                                                           |
|`ls`                               |To check the decompressed files from the 'data' archive                                  |
|`file data5.bin`                   |Filing the obtained file from the archive                                                |
|`mv data5.bin data5.tar`           |To rename the file 'data5.bin' to 'data.tar' to decompress teh tar compression           |
|`tar -xf data data5.tar`           |To decompress the tar compression                                                        |
|`ls`                               |To check the decompressed files from 'data5.tar' archive                                 |
|`file data6.bin`                   |To check teh next decompression to be made                                               |
|`mv data6 data6.tar`               |To rename file 'data6' to 'data6.tar' for decompression of tar                           |
|`tar -xf data6.tar`                |To decompress tar                                                                        |
|`ls`                               |To check the files obtianed from decompressed archive                                    |
|`file data8.bin`                   |To check filetype of data8.bin                                                           |
|`mv data8.bin data8.gz`            |To rename file 'data8.bin' to 'data8.gz' to decompress the gzip compression              |
|`gzip -d data8.gz`                 |To decompress the gzip compressio                                                        |
|`file data8`                       |To chek file type of file 'data8'                                                        | 
|`ct data8`                         |To read the content of ASCII file (human-readable file)                                  |
### What I learnt:
- To decompress the compression of gzip, bzip2 and tar, extensions of 'gz', 'bz2' and 'tar' respectively are required for the respectie files.
- `tar` compresses multiple files to form an archive where as 'gzip' and 'bzip2' compress singular files.

---

# Level 13 → 14
### Objective: To find the private SSH key stored in '/etc/bandit_pass/bandit14', only accessible by user bandit14
### What I thought and executed: 
1. I ran `ls` command to check which all files are inthe directory. I ran `cat HELP` and `cat sshkey.private`. Access denied for `cat sshkey.privatr`.
2. I ran `cat /etc/bandit_pass/bandit14` but access denied again. I realised that access is only for user bandit14.
3. I read about SSH/OpenSSH/keys on teh 'Helpful Reading Material' section on the official website [OverTheWire Bandit](https://overthewire.org/wargames/bandit/).
4. I ran `scp -p 2220 bandit13@bandit.labs.overthewire.org:~/sshkey.private .`. `scp` is Secure Copy Protocol that safely transfers files and directories between different systems over a network. This command translates to 'on that server logged in as bandit13, grab file sshkey.private from home directory'. The '.' at the end is to copy the file to my current directory o my local machine.
5. I ran `exit` to exit from 'bandit13' directory. Then on my local machine/VM I ran `ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220` where, 'ssh' is secure shell command, '-i sshkey.private' is used as my private key instead of the usual password, 'bandit14' is the user, 'bandit.labs.overtewire.org' is the remote server being entered and '-p 2220' is the port for bandit rather than the standar port 22 for `ssh` commands.
6. I ran into an error as 'sshkey.private' permissions (0640) are too open. For a private jey, it should have permissions that restrict usage of the file only to the owner, thus `chmod` command is used.
7. I ran `chmod 600 sshkey.private` (which should have been run before the ssh command) where 'chmod' is the command used, '6' is '-rw- i.e. only owner can read and write, '0' group gets nothing and last '0' for 'others get nothing'.
8. Then run ssh command again and obtain the password for level 14, that can be entered when trying to log into bandit14 level from the outside directly.
### What was required:
|Commands Required (in order)                                         |Puprose                                                    |
|---------------------------------------------------------------------|-----------------------------------------------------------|
|`ls`                                                                 |To list all files in home directory                        |
|`cat HINT`                                                           |To get idea of what all should be done in the level        |
|`scp -p 2220 bandit13@bandit.labs.overthewire.org:~/sshkey.private .`|To securley copy the file 'sshkey.private' to local machine|
|`chmod 600 sshkey.private`                                           |To change the persmissions of the file to match those of a private key|
|`ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220`|To ssh into the server using the sshkep.private instead of a password|
### What I leanrt:
- All passwords for the current levels (say L) are stored in files '/etc//bandit_pass/banditL' and can be accessed only by user banditL.
- Ports are like doors to the server building. Specific ports are for specific commands, like: 
    - port 22: default for SSH doors
    - port 80: HHTP
    - port 443: HTTPS
    - PORT 2220: bandit's custom SSH doors
- Private keys have limited permissions and SSH refuses to use private keys that aren't only accessible by users.

---

# Level 14 → 15
### Objective: To retrieve the passowrd by submitting password of current level to port 30000 on localhost
### What I thought and executed:
1. I ran `man` on suggested commands (`ssh`, `telnet`, `nc`, `openssl`, `s_client` and `nmap`) and figured that `nc` (netcat)is the way to go as it is used as a raw pipe between 2 machines over a network without any encryption.
2. I ran `nc localhost 30000` where 'localhost' is the machine to connect to and '30000' is the port.
3. It requested to enter the password of current level and returns output as the password for the next level.
### What was required:
|Commands Required (in order)|Purpose                                           |
|----------------------------|--------------------------------------------------|
|`nc localhost 30000`        |To connect with 'localhost' machine via port 30000|
### What I learnt:
- `nc` command is used to connect 2 machines on the network directly, without encryption.

---

# Leve 15 → 16
### Objective: To retrieve password for next level by submitting the password of current file to port 31000 on localhost using SSL/TLS encryption
### What I thought and executed:
1. I ran `man openssl`and figured `openssl s_client` command is to be used as `s_client` is like `nc` just wraped with SSL/TLS encryption. It opens a connection between host and port while letting us type and send data.
2. I ran `openssl s_client -connect localhost:31000` where, 'openssl' is the main command, 's_client' is the sub-command, '-connect' is the flag, 'localhost' is the host machine, ':' is the sperator and '31000' is the port.
3. It waits for me to enter the password of the current level as input and gives password of next level as the output.
### What was required:
|Commands Required (in order)               |Purpose                                                 |
|-------------------------------------------|--------------------------------------------------------|
|`openssl s_client -connect localhost:31000`|To establish connection between localhost and port 31000|
### What I learnt:
- `s_client` and `nc` differ only in the sense that one encrypts data with SSH/TLS while the other simply connects host and port.

---

# Level 16 → 17
### Objective: To retrieve password for next level by submitting password of current file to a listening port that speaks SSL/TSL in the range 31000-32000
### What I thought and executed:
1. A 'listening port' is an active port waiting for connection. Its like a door behind which someone is waiting to answer.
2. I am effectively looking for a 'port scanner' right now.
3. The `nmap` command is a port scanner, so I ran `namp -p 31000-32000 localhost` where 'nmap' is the command, '-p 31000-32000' is the port range and 'localhost' is the machine being scanned.It shows all the listed ports (in my caase,5: 31046, 31518, 31691, 31790 and 31960)
4. To check if they speak SSL/TSL, I ran the command `openssl s_client -connect localhost:port -ign_eof`. All but 2 ports (31518 and 31790) showed no result or returned my entered password of the current level as it is.
5. Before adding '-ign_eof' the system thought that right after passing data or its standard output, it was 'end of communication' thus would automatically close the route. '-ign_eof' stands for 'ignore end of file' which allows system to pause after sending all required data, thus comfortably allowing me to enter the password for this level or using the 'k' command when it read KEYUPDATE. 'k' command is to continue the system as it is and expect an output as well.
6. The port '31790' I got a passkey for the next level.
7. I googled this part, as to what to do with the passkey, because unlike level 13 → 14 where the passkey was already stored in a file, I had to make a file here and then move forward.
8. I coppied the entire passkey, from'---Banit to ---' using ctrl+c after selecting all of it. I ran `exit` to exit the bandit terminal.
9. I ran `nano bandit17.key` where 'nano' is a simple text editor that works in the terminal. On entering this, I pasted the passkey with ctrl+v, exitedit with ctrl+x 'yes' and 'continue'.
10. Then I ran `chmod 600 bandit17.key` to change its permisions making it fit for a private key that SSH can use.
11. I ran `ssh -i bandit17.key bandit14@bandit.labs.overthewire.org -p 2220`.
12. Once in the bandit17 server, I ran `cat /etc/bandit_pass/bandit17` to store the password of level 17 so that I can use it to enter the level externally via the normal SSH command.
### What was required:
|Commands Required (in order)|Purpose|
|----------------------------|-------|
|`nmap -P 31000-32000 localhost`|To scan for the listening ports|
|`openssl s_client -connect localhost:31790 -ign_eof`|To check SSL/TSL of the listening ports|
|`cope passkey`|To store it|
|`exit`|To exit the terminal|
|`nano bandit17.key`|To make a file bandit17.key, paste the passkey in it, ctrl+x to exit it|
|`chmod 600 bandit17.key`|To make it fit for usage as a private key by SSH|
|`ssh -i bandit17.key bandit17@bandit.labs.overthewire.org -p 2220`|To SSH into level17 via private key rather than a password|
|`cat /etc/bandit_pass/bandit17`|To store tha ctuall password for level 17 for logging in externally via SSH|
### What I learnt:
- Password for a level (say 17) is always stored in file '/etc/bandit_pass/bandit17'.
- The `nano` command is a simple text editor that works through the terminal.

---

# Level 17 → 18
### Objective: To find the password for the next level which is the only different line in file 'passwords.new' from the file 'passwords.old', both stored in the home directory
### What I thought andexecuted:
1. I ran `man diff` from the suggested commands on the official site [OverTheWire Bandit](https://overthewire.org/wargames/bandit/). This is a command that (without any specific options chosen) simply tells the difference in file2 from file1 if executed as `diff file2 file1`.
### What was required:
|Commands Required (in order)      |Purpose                                                               |
|----------------------------------|----------------------------------------------------------------------|
|`diff passwords.old passwords.new`|To identify the different lines in 'passwords.old' and 'passwords.new'|
### What I leanrt:
-

---

# Level 18 → 19
### Objective: To find the password for the next level stored in a file 'readme' on the homedirectory that has been hacked to log out as soon as you loggin.
### What I thought and executed:
1. On simply trying to run `ssh` command, '-bashrec' runs immediatley after the full shell is launched and logs me out of bandit..thus the 'bye bye!'.
2. So we can run the `cat readme` command as soon as we're in the server rather than after the full shell has logged in.
3. I googled how to do this and thus ran the command `ssh bandit18@bandit.labs.overthewire.org -p 2220 "cat readme"`. The command in "" runs immediately on the server.
### What was required:
|Commands Required (in order)|Purpose|
|----------------------------|-------|
|`ssh bandit18@bandit.labs.overthewire.org -p 2220 "cat readme"`|To run the `cat` readme command immeadiatley after `ssh` without waiting for the full shell to load|
### What I learnt:
- The command in "" runs immediately by bypassing the interactive login shell.

--- 

# Level 19 → 20
### Objective: To fin the password in'/etc/bandit_pass/banditlevel' after correctly executing the 'setuid binary' command in the home directory
### What I thought and executed:
1. I ran `ls` command, and got an 'executable file' i.e. a file that can be run as an individual programme.
2. I ran `./bandit20-do` where './' means 'run this file from current directory.
3. I read about 'setuid' on wikipedia as suggested in the 'Helpful Reading Material'.
4. I ran `./bandit20-do whoami` as suggested in the terminal output.
5. This command gives me access to files that only bandit20 has access to i.e. the `cat /etc/bandit_pass/bandit20` command.
6. So I ran `./bandit20-do cat /etc/bandit_pass/bandit20` to use the command `cat` while having the access of 'bandit20' via the executable file 'bandit20-do'.
7. These 2 commands don't work seperately, i.e. `./bandit20-do`, enter, and then `cat /etc/bandit_pass/bandit20` as when we execute the command `cat` seperatley, we are execute it as 'bandit19' user, who doesn't have access to '/etc/badndit_pass/bandit20'.
### What was required:
|Commands Required (in order)                 |Purpose                                                         |
|---------------------------------------------|----------------------------------------------------------------|
|`ls`                                         |To know which all files are in home directory                   |
|`./bandit20-do`                              |To execute the executable file 'bandit20-do'                    |
|`./bandit20-do whoami`                       |As suggested in the terminal output                             |
|`./bandit20-do cat /etc/bandit_pass/bandit20`|To access the password for level 20 by having access of bandit20|
### What I learnt:
- To execute executable files of name 'file', we run command `./file` which is 'execute the file 'file' in this directory.

---

# Level 20 → 21
### Objective: To recieve the password from a setuid binary after correctly executing it
### What I thought and executed:
1. I ran `ls` command to check the name of the executable setuid binary file in the home directory, it was 'suconnect'.
2. I ran `./suconnect` to see how the command works.
3. I ran `./suconnect password_of_level_20` which failed as this was the wrong syntax for executing this command.
4. 'suconnect' would read the password sent to a listening port, if it was the password for level 20, then it would give the password for level 21 in its output.
5. I ran `echo "0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO" | nc -l -p 1234` where, `echo` is a simple command that prints whatever is entered in the "". The '|' (pipleline), enters '0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO' i.e. the password to level 20 as input for the `nc` command.
6. The `nc` command (netcat) is the simplest way to open a port on localhost machine and send data to whatever it is connected to. The '-l' is for 'listen for incoming connection' and '-p' (lowercase 'p') is for the source port.
7. Then I ran `./suconnect 1234`. This was the wrong move, both these commands had to be run simultaneously. An anology for this could be, `./suconnect` dials a phonecall, `nc` picks up and speaks the password on port '1234'. These commands need to be run together as a process rather than successive commands.
8. There are 2 ways to do this:
    - Using the `tmux` command that creates multiple terminals, so both commands can be run at the same time, in different terminals.
      |Commands I ran for `tmux` approach|Purpose|
      |----------------------------------|-------|
      |`tmux`|To start 'tmux'|
      |Ctrl+b then " |To split it itno 2 panes|
      |`echo "0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO" \| nc -l -p 1234`| To be run in the top pane, for the password of the previous level to be given to port 1234|
      |Ctrl+b then arrow down|To switch to the bottom pane|
      |`./suconnect 1234`|To read the password of previous level from port 1234|
    - *shortcut* `echo "0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO" \| nc -l -p 1234 & ./suconnect 1234` to run both commands at same time, However this gave an error as th 'suconnect' was way faster than the echo and didnt find anything at the port 1234, thus failed. Then I ran
    `echo "0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO" \| nc -l -p 1234 & sleep 1 && ./suconnect 1234` allowing the system to pause for 1 second and then allowing 'suconnect' to read the password from the port 1234.
9. I went with the shortcut method for this one.
### What was required:
|Commands Required (in order)                                                            |Purpose|
|----------------------------------------------------------------------------------------|-------|
|`ls` |To know the name of the fiels to be used                                          |
|`./suconnect`|To know what the 'suconnect' command did                                  |
|`echo "0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO" \| nc -l -p 1234 & sleep 1 && ./suconnect 1234`|To read the password of the previous level from a listening port|
### What I learnt:
- In the syntax of the `man` pages of commands, things written in [] don't actually require to be entered in the terminal with the [].
- `echo` is a basic linux command/tool that prints simple texts or characters in written in "".
- `nc` or 'netcat' is the simplest command to open a port on localhost and to send data to whatever it is connected to.
- This level was a basic introduction to TCP client/server interaction.
- `&` allows 2 commands to be run simultaneously.
- `sleep 1` means allowing the system to pause for 1 second before executing the command on the right.

--- 

# Level 21 → 22
### Objective: To find the password for the next level by looking into '/etc/cron.d/' as a background process runs in intervals.
### What I thought and executed:
1. I ran `man cron` and came across a word 'daemon' which means a background process that runs independently of user interface as it performs tasks for the system.
2. Then I ran `cat /etc/cron.d/`, wich told me that this was a directory.
3. Since its a directory, I ran `cd /etc/cron.d/` to switch directories.
4. I ran `ls` to check the contents of this directory.
5. I ran `cat cronjob_bandit22` amongst all the other files (notably, 2 for levels 23 and 24, a few of other wargames etc).
6. In the output, a pattern '* * * * *' appeared which meant 'running every minute'. So I ran `cat /usr/bin/cronjob_bandit22.sh`.
7. Initially I thought that the hash tag it displayed was the password, so I quickly saved it to my laptop's designated file, exited the directory and ssh into level 23 only to realise while entering the password, that it was the wrong one. After trying for 5 times, I went back to the terminal output I had gotten and realised that maybe I had to cat another file's address that was printed in the terminal ouptu.
8. For that I had to run all the commands again to enter the directory '/etc/cron.d/'.
9. Then I ran `cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv`, which then revealed the actual password for level 23.
### What was required:
|Commands requried (in order)               |Purpose                                                  |
|-------------------------------------------|---------------------------------------------------------|
|`cat /etc/cron.d/`                         |In attempts to read '/etc/cron.d/'                       |
|` cd /etc/cron.d/`                         |To switch directories                                    |
|`ls`                                       |To check the contents of the new directory               |
|`cat cronjob_bandit22`                     |To read the relevant file for this level                 |
|`cat /usr/bin/cronjob_bandit22.sh`         |Followed the instructions in the terminal ouput          |
|`cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv`| To read the file address returned in the terminal output|
### What I leanrt:
- ALWAYS read the terminal output and follow the guidelines of the terminal output.

---

# Level 22 → 23
### Objective: To find the password for the next level by looking into '/etc/cron.d/' as a background process runs in intervals.
### What I thought and executed:
1. I ran `cat /etc/cron.d/`, it turned out to be directory again.
2. I ran `cd /etc/cron.d/` to switch directories.
3. I ran `ls` to check the contents of the new directory.
4. I ran `cat cranjob_bandit23` to read the relevant file of this level.
5. I did all the things manually asked in the terminal output including entering these commands word for word: 
    myname=$whoami
    mytarget=$(echo I am user $myname |md5sum | cut -d - - -f 1)
    echo "/etc/bandit_pass/$myname to /tmp/$mytarget
    cat /tmp/$mytarget
which was the **wrong** move, as it took 'whoami' as bandit22 by defualt, thus returned the password of this level.
6. After realising my mistake, I ran `echo "I am user bandit23" | md5sum | cut -d ' ' -f 1`, then recieved a 'hash' or series of characters.
7. Then before assuming these characters as my password, I ran `cat /tmp/8ca319486bfbbc3663ea0fbe81326349` and recieved the correct password for the next level.
### What was required:
|Commands Required (in order)                           |Purpose                                  |
|-------------------------------------------------------|-----------------------------------------|
|`cat /etc/cron.d/`                                     |In attempts to read '/etc/cron.d/'       |
|`cd /etc/cron.d/`                                      |To switch directories                    |
|`ls`                                                   |To read the contents of the new directory|
|`cat cranjob_bandit23`                                 |To read the relevant file for this level |
|`echo "I am user bandit23" \| md5sum\| cut -d ' ' -f 1`|                                         |
|`cat /tmp/8ca319486bfbbc3663ea0fbe81326349`            |                                         |
### What I learnt:
-

---

# Level 23 → 24
### Objective: To find the password for the next level by looking into '/etc/cron.d/' and following through with what is being executed
### What I thought and executed: 
1. I ran `cd /etc/cron.d/` to enter this directory.
2. I ran `ls` to see the different files in this directory.
3. I ran `cat cronjob_bandit24`, the relevant file to crack the password for the next level, i.e. level 24.
4. I ran `cat /usr/bin/cronjob_bandit24.sh` to read the content of this file.
5. Unlike previous levels, this level required a fake directory to be made ( as suggested on [OverTheWire: Bandit](https://overthewire.org/wargames/bandit/)), so I ran `mkdir /tmp/mydir` to create a temporary directory 'mydir' in tmp folder.
6. `cronjob` was going to run it's procedure every minute as user 'bandit24'. It read the contents of the fil in the specified address ('/var/spool/bandit24/foo/' as stated in the terminal output) and executed it if it was an 'executable' file.
7. As it runs the files with permissions of user 'bandit24', it has the permission to execute the command `cat /etc/bandit_pass/bandit24`. So the goal is to make a file having this command, store it in the specified location, modify its permission to 777 i.e. allowing the user, user's group and others permision to 'rwx' i.e. read, write and execute. (777 in binary stands for 111, so all permisions 'read', 'write' and 'execute' are turned 'on' with 1).
8. I ran `nano /tmp/mydir/myscript.sh` to create a text file in the directory 'mydir'. It opened to a simple text editor in the terminal where I typed, '#!/bin/bash' in line 1 and `cat /etc/bandit_pass/bandit24 > /tmp/mydir/password` where '>' sent the output of the first command to the *file* of teh address '/tmp/mydir/password' instead of the terminal.
9. I ran `chmod +x /tmp/mydir/myscript.sh` to make the file 'myscript.sh' an executable file. If this file wasen't 'executable' then it would just be a text file which would refuse to be run by cronjob, thus serving no purpose.
10. I ran `chmod 777 /tmp/mydir` to change the permissions of the directory to '777' as explained in point number 7.
11. I ran `cp /tmp/mydir/myscript.sh /var/spool/bandit24/foo/` to copy the content of the file 'myscript.sh' to the specified location. Its necessary to copy the content from an external file to the specified location instead of making everything in the specified location as in the terminal ouptut of `cat /usr/bin/cronjob_bandit24.sh` it states that it will execute and *delete* the files every minute, thus we will lose the file at the specified location. But having the commnd to store the password in an external file allows us to access the content of the file even after the orignal is deleted at the specified location.
12. Since `cronjob` runs its procedure of reading the files at the specified location and then deleting them every minute, I waited for 60 seconds before running the command `cat /tmp/mydir/password` to read the password that `cronjob` has stored here.
### What was required:
|Commands Required (in order)|Purpose|
|----------------------------|-------|
|`cd /etc/cron.d/`|To dwitch directories|
|`ls` |To look at the different files listed in the directory|
|`cat cronjob_bandit24`|To read the most relevant file for this level|
|`cat /usr/bin/cronjob_bandit24.sh`|To read the stored file|
|`mkdir /tmp/mydir`|To make a temporary directory|
|`nano /tmp/mydir/myscript.sh`|To make a file 'myscript.sh' in the new directory|
|'#!/bin/bash'  in line 1; `cat /etc/bandit24 > /tmp/mydir/password` in lin2|
|`chmod +x /tmp/mydir/myscript.sh`|To make the file executable|
|`chmod 777 /tmp/mydir`|To change the permissions of the directory to make it accessible and editable to everyone|
|`cp /tmp/mydir/myscript.sh /var/spool/bandit24/foo/`|To copy the file to desired location|
|`cat /tmp/mydir/password`|To be run **1 minute AFTER** previous command ran, to read the password for the next level from file 'password'|
### What I learnt:
- Permissions in Linux are split into 3 groups: 'owner', 'owner's group' and 'others' ('other's' includes everyone else including owner). There are 3 permissions 'read', 'write' and 'execute'. 
- 777 in binary is 111 which means the permission 'rwe' (read, write and execute) are given to all 3, 'owner', 'owner's group' and 'others'.
- `mkdir` is command that allows you to make your own directory at desired location.
- `+x` optio in `chmod` command is for maing the selected file 'executable'.
- '>' redirects, i.e. sends output of first command to another *file* whose address is linked after it.
  '|' (pipeline) send the output of first command to another *command* which is written after it.
---

# Level 24 → 25
### Objective: To retrieve the password for the next level as output obtained after entering password to current level, along with a specific numeric 4-digit pincode to port 30002
### What I thought and executed:
1. I first clumsily tried `echo "gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8" | nc localhost 30002` (which was without the 4 digit secret pincode) to see what type of output it displayed. It was an interactive output, asking for the 4 digit pin code which I did not know then.
2. I had two choices now:
    - Manually enter all possible 4 digit numeric pincodes from 0000 to 9999, as in using 'bruteforce' to get the correct pincode.
    - In a Nano file, use a 'loop' and `nc` and pipeline the results of the loop (which will be a pincode from 0000 to 9999) to the port 30002 using `nc localhost 30002`.
    The second method is shorter, more efficient and works best for even larger data.
3. The file will also have to be made executable using `chmod +x file_adddress_and_name` so that the shell can execute the loop and keep generating all possible 4 digit pincodes from 0000 to 9999.
4. I googled the syntax for the loop. I ran `nano /tmp/bruteforce.sh` to make a file of the filename 'bruteforce.sh'.
   In the file I typed:
```
#!/bin/bash
    for i in $(seq -w 0000 9999); do
        echo "gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8 $i"
    done | nc localhost 30002
```
5. Then I did `ctrl + x` to close the file, `yes` and `enter`.
6. I ran `chmod +x /tmp/bruteforce.sh` to make the file 'bruteforce.sh' an executable file. 
7. I ran `/tmp/bruteforce.sh` to execute this file. In the terminal ouptut, 'wrong' will be printed continuously untill the correct four digit numeriv pincode is entered. It will then display the password for the next level in the terminal output.
### What was required:
|Commands Required (in order) |Purpose        |
|-----------------------------|------------------------------------------------------------------|
|`nano /tmp/bruteforce.sh`|To create a file 'bruteforce.sh' an entered the required data as discussed in point 4 of previous section|
|`chomd +x /tmp/bruteforce.sh`|To make the file executable|
|`/tmp/bruteforce.sh`|To execute the executable file 'bruteforce.sh'   |
### What I learnt:
- The extension on file 'bruteforce.sh', i.e. '.sh' is just for us humans, so that at a glance we can tell that this is a shell script. For the system, the first line of this file, i.e. `#!/bin/bash` tells the system that this a shell script.
- 'tmp' is the temporary directory in Linux that stores all temporary files.
---

# Level 25 → 26
### Objective: To use passkey to connect to next level, but shell for user bandit26 isn't `/bin/bash`
### What I thought and executed:
1. I ran `man more`. The `ls` and `more bandit26.sshkey`. There is little but crucial difference in `more`, `cat` and `cat` (disscussed in 'What I learnt:' section). 
2. I ran `cat /etc/shells` to check the available valid login shells. `more` was being used.
3. I ran `cat bandit26ssh.key` and copied the entire context and exited bandit25 to enter my localmachine.
4. Then I ran `nano bandit26.sshkey`, pasted the copied contexts, `ctrl+x` and closed it.
5. I ran `chmod 600 bandit26.sshkey` to change permissions of this file to that of a private ssh key file.
6. Through my local machine, I ran `ssh -i bandit26.sshkey bandit26@bandit.labs.overthewire.org -p 2220` with the terminal shrunken to 1-2 lines. 
7. If the command is entered without shrinking the terminal window size to 1-2 lines, then `more` doesn't stop for keyboard input, and the file is written in such a way that after loading bandit26, it immediately kicks us out of there.
8. Something like `more(15%)` should show up. Then I typed `v` to open the `vi` editor (an editor similar to `nano`).
9. In the `vi` editor I typed `:set shell=/bin/bash` to change the file to a normal bash fileand pressed enter.
10. To activate it, I typed `:shell` and pressed enter. Now, the file type is bash (`more` also changes to green and shows like `--More--`).
11. Now, I we are in bandit26. To obtain password of curreny level, I ran `cat /etc/bandit_pass/bandit26`.
### What was required:
|Commands (in order)|Purpose|
|-------------------|-------|
|`ls`|To list the files in home directory|
|`cat bandit26.sshkey`|To read the file bandit26.sshkey, copying its entire content, and exiting back to local machine|
|`nano bandit26.sshkey`|To make file bandit26.sshkay, paste the copied content, and exit by `ctrl+x`|
|`chmod 600 bandit26.sshkey`|To change the permissions of the file to that of private sshkey file|
|`ssh -i bandit26.sshkey bandit26@bandit.labs.overthewire.org -p 2220`|To ssh into next level, via private key and terminal window shrunken to 1-2 lines|
|`v`|To enter the `vi` editor|
|`:set shell=/bin/bash`|To change file type to bash|
|`:shell`|To activate above mentioned change|
|`cat /etc/bandit_pass/bandit26`|To read the file for password of current level|
### What I learnt:
- |`cat`|`more`|`less`|
  |-----|------|------|
  |Dumps everything at once (even 1000 lines), user screen stops at the end of the document|Displays 1 screenfull of content, waits for us to read, then click `space` to continue|*`less` is 'more' but better* ~ You can scroll up and down, search with `i` and quit with `q`|
- `vi` is another text editor like `nano` that opens up in the terminal.
---

# Level 26 → 27
### Objective: To grab password of level 27 after entering shell from level 25
### What I thought and executed:
1. I ran `ls`.
2. I ran `cat bandit27-do`. After reading the terminal output, I found out that using `bandit27-do` I gain access of bandit27, meaning I can easily read those files that only bandit27 has access to while being in bandit26.
3. I ran `./bandit27-do cat /etc/bandit_pass/bandit27` to read the password of next level, with the access of level 27, through the file bandit27-do present in this directory (./).
### What was required:
|Commands Required (in order)|Purpose|
|----------------------------|-------|
|`ls`|To see which all files are in the home directory|
|`cat bandit27-do`|To find out what this file does|
|`./bandit27-do cat /etc/bandit_pass/bandit27`|To read password for level 27|
### What I leanrt:
-
---

# Level 27 → 28
### Objective: To find password for next level by cloning a repository from given URL and reading its content
### What I thought and executed:
1. I ran `sudo apt install git` to install git in the terminal.
2. I ran `git clone "ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo"` to clone the repo to my local machine.
3. I ran `ls` to see the cloned files.
4. I ran `cd repo` to switch to 'repo' directory. 
5. I ran `ls` to check files in 'repo'.
6. I ran `cat README` to read the file 'README' and get the password.
### What was required:
|Commands Required (in order)|Purpose|
|----------------------------|-------|
|`sudo apt install git`|To install git on the terminal in the vm|
|`git clone "ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo"`|To clone the desired file from specified url to current directory|
|`ls`|To check the files in the cloned files|
|`cd repo`|TO switch to the cloned repository|
|`ls`|To check the list of files in 'repo' directory|
|`cat README`|To read the file 'README'|
### What I learnt:
- **repository** = **directory** = **folder** 
---

# Level 28 → 29
### Objective: To find password for next level by cloning a repository from given URL and reading its content
### What I thought and executed:
1. I ran `git clone "ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo"` to clone the required repo from mention URL at the official site [OverTheWire: Bandit](https://overthewire.org/wargames/bandit/).
2. I ran `ls` and `cd repo` along with `ls README.md`.
3. It shoed password 'xxxxxxx', i.e. redacted.
4. GIT tracks changes made over time. The password was orignally there, then someone made a commit (updated it), and redacted the password. So, we need to see past commits, so I ran `git log`. 
5. It showed 3 comments, out of which I ran `git show <comment hash>` (comment hash written plainly, without the <>) to see the details of any suspicious commit (commit no. 2).
6. The password was revealed in the commit.
### What was required:
|Commands Required (in order)|Purpose|
|----------------------------|-------|
|`git clone "ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo"`|To clone required repo on local machine|
|`cd repo`|TO switch directories to 'repo'|
|`ls`|To check teh files in 'repo'|
|`cat README.md`|To read file 'README.md'|
|`git log`|To review past commits made|
|`git show <>`|To check details of specified commtits|
### What I learnt:
- When dealing with `git`, one of the 2 most important tools to use everytime is `git log`.
- (Already mentioned, but relevant anyways)Ubuntu doesn't require extensions in files, its only for humands to know at a glance what type of file it is. Example, in 'README.md', extension 'md' is for users to know that its a markdown file, Ubunu knows its a markdown file from its content.

# Level 29 → 30
### Objective: To obtain the password of next level by cloning required repository and reading its content
### What I thought and executed:
1. I ran `git clone "ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo"`.
2. I ran `cd repo`, `ls`, `cat README.md`. It said password hasen't been decided yet.
3. I ran `git log` and ran `git show <>` on all suspicious commits, but got nothing.
4. I asked Claude about git, and along with `git log`, the second most important tool is `git branch -a` which tells us of all the other branches git has and a few of them could still be unaltered, and have the password.
5. 'dev' is where the actual work is done before being cleaned, there is a high chance that password is still there in dev. So I ran `git checkout origin/dev`.
6. Now I was in 'dev' branch, so I ran `cat README.md` again and got the password.
### What was required:
|Command Required (in order)|Purpose|
|---------------------------|-------|
|`git clone "ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo"`|To clone req repo from given URL|
|`cd repo`|TO switch directories|
|`cat README.md`|To read the file 'README.md'|
|`git branch -a`|To see other branches, where password is still possible present|
|`git checkout origin/dev`|TO go to 'dev' branch|
|`cat README.md`|To read the file README.md while being in the de branch|
### What I leanrt:
- **2 Most Important** tools while dealing with `git` are: **`git log`** and **`git branch -a`**.
---

# Level 30 → 31
### Objective: To find password for next level by cloning requried repo via git and reading its content
### What I thought and executed:
1. I ran `git clone "ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo"` along with `cd repo`, `ls`, `cat README.md`. The oassword was not there.
2. I ran 2 trusted tools of git `git log` and `git branch -a` but nothing useful.
3. I ran `git tag` to see all the added tags, where `tag` is another essential tool of git.
4. Tags are labels attached to specific points in a repository that make working with a repo much easier.
5. It showed 'secret', so I ran `git show secret` and the password appeared.
### What was required:
|Commands Required (in order)|Purpose|
|----------------------------|-------|
|`git clone "ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo"`|To clone repo|
|`cd repo`||
|`ls`||
|`cat README.md`||
|`git tag`|TO see names of all added tags in the repo|
|`git show secret`|To read the tag 'secret'|
### What I learnt:
- Along with `git log` and `git branch -a`, tags are also important git features that allow easy understanding of the content of the repo.
---

# Level 31 → 32
### Objective: TO find the password of next level by cloning a repo with given URL and reading its content
### What I thought and executed:
1. I ran `git clone "ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo"` along with `cd repo`, `ls`, `cat README.md`.
2. In the READMEmd, its said to push a file to the repository to get the password.
3. So I ran `echo "May I come in?" > key.txt` to create teh file key.txt with the content 'May I come in?' in one command.
4. `echo` command reprints the thing in "", this time, it was sent to a file 'key.txt' (if it existed before, then it would be added in the contents, if not, then a new file named 'key.txt' was made) using the `>`.
5. I ran `git add -f key.txt` to include this file in the next commit. The -f flag means **force**. Without it, git would have ignored the txt file as a file '.gitignore' by defualt is there in that repo that explicitly ignored .txt files.
6. I ran `git commit -m "add key"`, but it required changes and confirmations in teh configeration so I ran `git config --global user.email "a@a.com"` and `git config --global user.name "a"` as the names and emails didnt matter.
7. I re-ran `git commit -m "add key"` and then `git push origin master`. The password was printed in the output along with a lot of extra things.
### What was required:
|Commands Required (in order)|Purpose|
|----------------------------|-------|
|`git clone "ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo"`|To clone req repo|
|`cd repo`||
|`ls`||
|`cat README.md`||
|`echo "May I come in?" > key.txt`|To make the file key.txt and add its content in one command|
|`git add -f key.txt`|To make it include key.txt in next commit, and if flag to forcefully include the .txt |
|`git commit -m "add key"`|To mention the commit made|
|`git config --global user.email "a@a.com"`|To change and confirm configerations before commiting finally|
|`git config --global user.name "a"`|TO change and confirm configerations before commiting finally|
|`git commit -m "add key"`||
|`git push origin master`|TO push the commits into the repo thorugh the master branch|
### What I learnt:
- We could have made a new file 'key.txt' using `nano` and then endered the text 'May I come in?' and it would have worked fine. But by using `echo "May I come in?" > key.txt` we smartly used the commands and finished the job in a single command.
---

# Level 32 → 33
### Objective: Find the password for the last time for that last level
### What I thought and executed:
1. After using `ssh` and the password for this level, the interface looked different. It wasen't normal shell script as there was no `$` in the terminal before keyboard input, instead there was `>`. In the terminal introduction it said this was UPPERCASE Shell, where everything entered would automatically be converted to uppercase.
2. This meant that running `ls` wouldn't work as the shell would take it as `LS` which is nothing.
3. I had no prior knowledge regarding this, so I googled it and found that the variable `$0` isnt affected by this UPPERCASE Shell as its a special variable. On entering this into the terminal, the terminal shifts to normal Shell script as teh `$` appears.
4. I ran `whoami` and surpisingly, it read bandit33. I asked Claude why this was the case.
5. UPPERCASE Shell is a setuid binary owned by bandit33. So, on entering `$0`, we escaped the UPPERCASE Shell as a new Shell script expanded and the permissions of UPPERCASE Shell were inherited by this new shell.
6. We have permissions of bandit33 user, so `cat /etc/bandit_pass/bandit33` is readable.
### What was required:
|Commands Required (in order)|Purpose|
|----------------------------|-------|
|`$0`|To return to normal Shell script from UPPERCASE Shell|
|`whoami`|To check who the user is of this newly made Shell script|
|`cat /etc/bandit_pass/bandit33`|To read password of level 33|
### What I learnt:
- `$0` is a special variable (on which UPPERCASE Shell doesnt work) that exapanded to form a new normal Shell script (having `$` in the start instead of `>`). In this process, permission of level 33 were also passed onto the newly made Shell script as UPPERCASE Shell is a setuid binary belonging to level 33.
---
# End of Levels !
---