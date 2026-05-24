# Level 0 → 1
### Objective:  Find the password for level 1 stored in a file readme located in the home directory.
### What I thought and executed:
1. Since I only knew the `man` command then, I ran `man` on the suggested commands (`ls`, `du`, `cat`, `file`, `cd`(no `man cd` exists) and `find`) in the official site for overthewire bandit i.e. [OverTheWire Bandit](https://overthewire.org/wargames/bandit/).
2. `ls` lists all the files (readable/nonreadable) present in the current directory.
3. `cat` reads the content of selected file and displays output in the terminal .
### What was required:
| Command Required (in order)   | Purpose                                                      |
|-------------------------------|--------------------------------------------------------------|
|`ls`                           | To confirm that a file 'readme' exists in the directory.     |
|`cat readme`                   | To read the file 'readme' for read-able content              |
### What I learnt:
- When you SSH into Bandit, you land in the home directory. I initially wasted time trying to find it, only to realise I was there all along.
- Using `man` command on the suggested command from the official link of OverTheWire Bandit is the way to go.
- `ssh` (Secure Shell) is a command that helps you securely connect to remote servers across a network. In `bandit1@bandit.labs.overthewire.org -p 2220`, *bandit1@bandit.labs.overthewire.org* is the server address and *-p 2220* is the port address.

---

# Level 1 → 2
### Objective: Find the password for level 2 stored in a file '-' located in the home directory.
### What I thought and executed:
1. To confirm that a file '-' exists in the home directory, I ran `ls`, and surely it was there.
2. To read its contents I ran `cat -`, only to freeze my terminal and I had to close it and re-open it.
3. Then I read in the 'Helpful Reading Material' section on [OverTheWire Bandit](https://overthewire.org/wargames/bandit/), that files beginning with '-' pose a problem to a few Linux commands, including `cat`. The correct way to run `cat` on these file names or any file names for that matter is `cat ./filename`.
### What was required:
|Command Required (in order)  | Purpose                                                |
|-----------------------------|--------------------------------------------------------|
|`ls`                         |To confirm that a file '-' exists in the home directory |
|`cat ./-`                    |To read the file '-' for the password                   |
### What I learnt:
- File names starting with '-' pose a problem to a few Linux commands. `cat ./-` works where '.' is for current directory, '/' is a directory separator and '-' is a filename.
- `-` is a Unix convention for stdin (standard input), so `cat -` waits for keyboard input, causing the terminal to freeze.

---

# Level 2 → 3
### Objective: Find the password for level 3 stored in a file '---spaces in this filename--' located in the home directory.
### What I thought and executed:
1. I ran `ls` command to confirm that a file 'readme' exists in this directory.
2. I ran `cat ./--spaces in this filename---`. This failed as it took '---spaces', 'in', 'this' and 'filename---' as different filenames which obviously didn't exist in the home directory.
3. I read the 'Helpful Reading Material' section on the [OverTheWire Bandit](https://overthewire.org/wargames/bandit/) for this particular level. 
4. I got 2 solutions:
    - Instead of `cat ./---spaces in this filename---`, I ran `cat ./---spaces\ in\ this\ filename---` which tells the system that the spaces followed after '\' be treated as a character in the filename rather than as separators.
    - *shortcut* : Press tab after './---spaces'. The system automatically types the file matching this initial name with the required additions of '\' wherever required. However this method fails when there are multiple files with the same initial filename.
### What was required:
| Commands Required (in order)            |                                                                                              |
|-----------------------------------------|----------------------------------------------------------------------------------------------|
|`ls`                                     |To confirm that a file 'readme' exists in the home directory                                  |
|`cat ./---spaces\ in\ this\ filename---` |To read the content of the file '---spaces in this filename---' appropriately for the password|
### What I learnt:
- While using Linux commands (like `cat`), filenames beginning with '-' or having spaces in them have to be written differently as they pose a problem to the shell as it takes them as different characters separated with a space. 
- '/' is used to let the system know that the following space is to be used as a charcters rather than a separator, it is the same while writing Markdown aswell. 

---

# Level 3 → 4
### Objective: Find the password for level 4 stored in a hidden file in the 'inhere' directory
### What I thought and executed:
1. The `find` command is used to search for files and directories on the server.
2. I ran the command `find [inhere]`. No results came up as i had entered the wrong syntax, no brackets are to be used, simply `find inhere`.
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
- `ls` can list read-able files from text to extension files, directories, links, characters etc.
- If on using `ls`, a file comes in blue color, means its a directory.
- `ls -a` can list hidden files.
- Hidden files are just files that begin with fullstop (.).

---

# Level 4 → 5
### Objective: Find the password for level 5 stored in human-readable file in the 'inhere' directory
### What I thought and executed: 
1. I ran `cd inhere` to switch directories.
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
- Using `./*` on various Linux commands saves time and effort.

---

# Level 5 → 6
### Objective: To find the password for level 6 stored in a directory in 'inhere' directory with '1033 byte size', 'not executable' and 'human readable'.
### What I thought and executed:
1. I ran `cd inhere` to switch directories.
2. I ran `file ./*` and got 19 'maybehere' directories.
3. Now we need a directory that is human readable (ASCII text), file size 1033 bytes (`du` command can help) and non executable.
4. We can `cd ./*` every directory, which is long and tough task.
5. I ran `man find` to figure out how to use specifications like size. After `man find`, you can type '/size' to find the keyword 'size' in the entire manual page.
6. For the 'non executabele' file ( a file that can't be run as a programme in itself) using `! -executable` works.
7. I finally ran `find . -size 1033c ! -executable` where, '.' to find in the current directory ('inhere'), '-' used for different criterias applied (like size), 'c' to specify bytes and '!' for 'non'.
### What was required:
|Commands Required (in order)       | Purpose                                                        |
|-----------------------------------|----------------------------------------------------------------|
|`cd inhere`                        |To switch directories from home directory to 'inhere' directory |
|`find . -size 1033c ! -executable` |To find a directory of size 1033 bytes and non executable       |
|`cd maybehere07`                   | To switch to desired directory                                 |
|`file ./*`                         |To check the human readable file (ASCII plain text)             |
|`cat file2`                        |To read the desired file for the required password              |
### What I learnt:
- Many further criterias like 'size' 'executable' etc can be applied to `find` command for desired result separated by  '-'.
- '/word' can be type in the manual page of the `man` command to search for keywords regarding chosen command.
- '!' is for negating commands like 'non executable files'.

---

# Level 6 → 7
### Objective: Find the password for level 7 stored in a file somewhere on the server having properties- owned by owner 'bandit7', group 'bandit6' and '33 byte' in size
### What I thought and executed:
1. I ran `man find` and searched '/user' and '/group' to figure out how to include these specifications in the find.
2. I finally ran `find /-size 33c -group bandit6 -user bandit7` where '/' searches the entire server, '-' separates the criterias, '33c' is for 33 bytes ('c' in Linux is for bytes).
### What was required:
|Commands Required (in order)                   | Purpose                                  |
|-----------------------------------------------|------------------------------------------|
| `find /-size 33c -group bandit6 -ser bandit7` |To find the file with these specifications|
|`cat ./filename`                               |To read the desired file for the password.|
### What I learnt:
- '/' searches the entire server.
- '.' searches the current directory.
-  Using '/' in the `man` pages of command allows you to search specific keywords.

---

# Level 7 → 8
### Objective: Find the password for level 8 stored in a file 'data.txt' next to the word 'millionth'
### What I thought and executed:
1. I ran `man` on suggested commands (`man`, `grep`, `sort`, `uniq`, `strings`, `base64`, `tr`, `gzip`, `bzip2` and `xxd`) to find a command that searches based off of patterns or keywords.
2. I ran `grep millionth data.txt` in the format 'grep whattosearch wheretosearch'.
3. I got the result and the password was right next to 'millionth'.
### What was required:
|Commands Required (in order)        |Purpose                                                   |
|------------------------------------|----------------------------------------------------------|
|`grep millionth data.txt`           |To search for the word 'millionth' in the file 'data.txt' |
### What I learnt:
- Running `man` command on the suggested commands of that level on [OverTheWire Bandit](https://overthewire.org/wargames/bandit/) helps learning in the long run as we get used to reading large amount of data which is necessary in the security field.
- `grep` command is used to search for characters in a file.

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