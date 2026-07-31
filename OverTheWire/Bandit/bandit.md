# Level 0 → 1
### Objective: Find the password for level 1 stored in a file readme located in the home directory.
### What I thought and executed:
1. I ran `man` on the suggested commands (`ls`, `du`, `cat`, `file`, `cd` (no `man cd` exists) and `find`) in the official OverTheWire Bandit site, i.e. [OverTheWire Bandit](https://overthewire.org/wargames/bandit/).
2. `ls` lists all the files readable/nonreadable present in the current directory.
3. `cat` reads the content of a selected file and displays output in the terminal.
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
2. To read its contents, I ran `cat -`. This froze my terminal.
3. I read in the 'Helpful Reading Material' section on [OverTheWire Bandit](https://overthewire.org/wargames/bandit/), that files beginning with '-' pose a problem to a few Linux commands, including `cat`. The correct way to run `cat` on these file names is `cat ./filename`.
### What was required:
|Command Required (in order)  | Purpose                                                |
|-----------------------------|----------------------------------------------------------|
|`ls`                         |To confirm that a file '-' exists in the home directory |
|`cat ./-`                    |To read the file '-' for the password                   |
### What I learnt:
- `cat -` freezes the terminal as `-` is a Unix convention for stdin (standard input), so `cat -` waits for keyboard input, causing the terminal to freeze.
- `cat ./-` works (where '.' is for the current directory, '/' is a separator, `./` allows `cat` to search the current directory) as it tells the shell to interpret `-` as a **path** rather than a flag/option.
---

# Level 2 → 3
### Objective: Find the password for level 3 stored in a file 'spaces in this filename' located in the home directory.
### What I thought and executed:
1. I ran the `ls` command to confirm that a file 'spaces in this filename' exists in this directory.
2. I ran `cat ./spaces in this filename`. This failed as it took 'spaces', 'in', 'this', and 'filename' as different filenames, which obviously didn't exist in the home directory.
3. I read the 'Helpful Reading Material' section on the [OverTheWire Bandit](https://overthewire.org/wargames/bandit/) page for this particular level.
4. I found two solutions:
    - Instead of `cat ./spaces in this filename`, I ran `cat ./spaces\ in\ this\ filename`, which tells the shell to treat the space following `\` as part of the filename rather than a separator.
    - *shortcut*: Press tab after './spaces'. The shell automatically types the file matching this initial name with the required additions of `\` wherever required. However, this method fails when there are multiple files with the same prefix.
### What was required:
| Commands Required (in order)            |Purpose                                                                                       |
|-----------------------------------------|----------------------------------------------------------------------------------------------|
|`ls`                                     |To confirm that a file 'readme' exists in the home directory                                  |
|`cat ./spaces\ in\ this\ filename`       |To read the content of the file 'spaces in this filename' appropriately for the password|
### What I learnt:
- The shell by default interprets spaces as argument separators and `-` as a flag prefix. Thus, while writing filenames, *spaces* and `-` are preceded by `\`.
- `\` is used to let the system know that the following space is to be used as a character rather than a separator.
---

# Level 3 → 4
### Objective: Find the password for level 4 stored in a hidden file in the 'inhere' directory
### What I thought and executed:
1. The `find` command is used to search for files and directories on the server.
2. I ran the command `find [inhere]` — *incorrect syntax; brackets are not used.* Simply `find inhere` works.
3. I ran `ls` in my home directory in hopes that it would read the content of all the directories, which was a rookie mistake. Since `man cd` didn't exist, it took me some googling to realise that the `cd` command is used to change directories.
4. I ran `file inhere` to confirm that it's a directory (it showed 'inhere' in blue).
5. I ran `cd inhere` followed by `ls` in the inhere directory. No results for `ls` as it was a hidden file.
6. I ran `ls -a` in the inhere directory, as this command lists all hidden files as well.
7. Hidden files in Linux are just files that begin with a full stop (.).
8. Then I ran `cat` on the hidden file to read its content.
### What was required:
|Commands Required (in order)|Purpose                                             |
|----------------------------|----------------------------------------------------|
|`cd inhere`                 |To switch from the home directory to the 'inhere' directory |
|`ls -a`                     |To list hidden files in the directory               |
|`cat filename`              |To read the content of the file                     |
### What I learnt:
- While using the `file` command, no need to use [ ] for the filename — that's the wrong syntax; instead `file filename` is correct.
- `ls` can list readable directory entries.
- By default in most terminals, `ls` colour-codes output, with **directories typically shown in blue**.
- `ls -a` can list hidden files.
- Hidden files are just files that begin with a full stop (.).

---

# Level 4 → 5
### Objective: Find the password for level 5 stored in a human-readable file in the 'inhere' directory
### What I thought and executed:
1. I ran `cd inhere`.
2. There were a number of files. There are 2 options:
    - Run `file` on all individual files until I get an *ASCII* file, which is the human-readable file. This method works but isn't efficient when dealing with a large number of files.
    - Run `file ./*`. This command files/categorises each file type in the current directory. '.' for this directory, '/' as a separator and '*' for everything.
### What was required:
|Commands Required (in order)|Purpose                                                            |
|----------------------------|-------------------------------------------------------------------|
|`cd inhere`                 |To switch directories to 'inhere' from the home directory              |
|`file ./*`                  |To check file types of all files in the current 'inhere' directory |
|`cat filename`              |To read the filename for the password                              |
### What I learnt:
- `*` is a *glob/wildcard* that the shell expands to all filenames in the current directory.
- `./*` expands to all files in the current directory, passing them as arguments to the command.

---

# Level 5 → 6
### Objective: To find the password for level 6 stored in a directory in the 'inhere' directory with a '1033 byte size', 'not executable', and 'human readable'.
### What I thought and executed:
1. I ran `cd inhere` to switch directories.
2. I ran `file ./*` and got 19 'maybehere' directories.
3. Now I needed a directory that is human-readable (ASCII text), has a file size of 1033 bytes (`du` command can help) and is non-executable.
4. I could `cd` into every directory one by one, which is a long and tedious task.
5. I ran `man find` to figure out how to use specifications like size. After `man find`, you can type '/size' to find the keyword 'size' in the entire manual page.
6. For the 'non-executable' file (a file that can't be run as a program in itself), using `! -executable` works.
7. I finally ran `find . -size 1033c ! -executable` where '.' is to find in the current directory ('inhere'), '-' is used for different criteria applied (like size), 'c' is to specify bytes and '!' is for 'non'.
### What was required:
|Commands Required (in order)       | Purpose                                                        |
|-----------------------------------|------------------------------------------------------------------|
|`cd inhere`                        |To switch directories from the home directory to 'inhere' directory |
|`find . -size 1033c ! -executable` |To find a file of size 1033 bytes and non-executable       |
|`cd maybehere07`                   | To switch to desired directory                                 |
|`file ./*`                         |To check the human readable file (ASCII plain text)             |
|`cat file2`                        |To read the desired file for the required password              |
### What I learnt:
- Many further criteria like 'size', 'executable' etc. can be applied to the `find` command where `-` is a **flag prefix** for each individual option.
- '/word' can be typed in the manual page of the `man` command to search for keywords regarding the chosen command.
- '!' is for negating criteria, like 'non-executable files'.

---

# Level 6 → 7
### Objective: Find the password for level 7 stored in a file somewhere on the server having properties — owned by owner 'bandit7', group 'bandit6' and '33 bytes' in size
### What I thought and executed:
1. I ran `man find` and searched '/user' and '/group' to figure out how to include these specifications in `find`.
2. I ran `find / -size 33c -group bandit6 -user bandit7` where '/' searches the entire server, '-' separates the criteria, '33c' is for 33 bytes ('c' in Linux is for bytes).
3. `find /` will return many **permission denied** errors for directories that user *bandit6* can't access.
### What was required:
|Commands Required (in order)                   | Purpose                                  |
|-----------------------------------------------|-------------------------------------------|
| `find / -size 33c -group bandit6 -user bandit7` |To find the file with these specifications|
|`cat ./filename`                               |To read the desired file for the password.|
### What I learnt:
- '/' is the **root of the filesystem**. `find /` searches from the root directory downward, covering the entire filesystem.
- '.' searches the current directory.
- Using '/' in the `man` pages of a command allows you to search for specific keywords.

---

# Level 7 → 8
### Objective: Find the password for level 8 stored in a file 'data.txt' next to the word 'millionth'
### What I thought and executed:
1. I ran `man` on the suggested commands (`man`, `grep`, `sort`, `uniq`, `strings`, `base64`, `tr`, `gzip`, `bzip2` and `xxd`) to find a command that searches based on patterns or keywords.
2. I ran `grep millionth data.txt`.
3. I got the result, and the password was right next to 'millionth'.
### What was required:
|Commands Required (in order)        |Purpose                                                   |
|------------------------------------|------------------------------------------------------------|
|`grep millionth data.txt`           |To search for the word 'millionth' in the file 'data.txt' |
### What I learnt:
- Running `man` on the suggested commands for each level on [OverTheWire Bandit](https://overthewire.org/wargames/bandit/) helps learning in the long run, as we get used to reading large amounts of documentation, which is necessary in the security field.
- `grep` is used to search for patterns (regular expressions) in files.

---

# Level 8 → 9
### Objective: Find the password for level 9 stored in a file 'data.txt' as the only line of text that appears once
### What I thought and executed:
1. I ran `man` on the suggested commands for this level; `sort` and `uniq` were to be used, but I didn't know how they were used together.
2. I read the page linked under 'Helpful Reading Material' for 'Pipelines and Redirections' and learnt that '|' is used for pipelining.
3. Pipelining refers to the process where the output of the first command is used as input for the second command.
4. I ran `sort data.txt | uniq -u`, where 'sort data.txt' sorts the data so identical lines are adjacent, '|' pipelines the result of `sort data.txt` into `uniq -u`, `uniq` is a command that filters based on adjacent repeated lines, and `-u` is for 'print lines that appear only once'.
### What was required:
|Commands Required (in order)        | Purpose                                                               |
|------------------------------------|-------------------------------------------------------------------------|
|`sort data.txt \| uniq -u`           |To sort the file 'data.txt' and find the lines that appear only once. |
### What I learnt:
- '|' is the pipeline operator that sends the output of the first command into the input of the second command.

---

# Level 9 → 10
### Objective: Find the password for level 10 stored in a file 'data.txt' among a few human-readable strings preceded by a number of '=' signs
### What I thought and executed:
1. 'Human-readable strings' refers to text that is not binary or otherwise non-human-readable.
2. I figured the `strings` command would be used to extract the readable strings in 'data.txt', and `grep` to search for the multiple '===' characters.
3. There were 2 methods:
    - `strings data.txt` and then manually read the strings, find the ones that start with "===", and read the password from the large output.
    - `strings data.txt | grep "==="`, which is a faster and more efficient way when dealing with large files.
4. The pipeline '|' would again feed the output of `strings` as the input of `grep`.
5. I ran `strings data.txt | grep "==="`.
### What was required:
|Commands required (in order)    |Purpose                                                               |
|--------------------------------|--------------------------------------------------------------------------|
|`strings data.txt \| grep "==="` |To search for the specific string pattern "===" in data.txt |
### What I learnt:
- There are combinations of commands that reduce the required effort to a minimum.

---

# Level 10 → 11
### Objective: Find the password for level 11 stored in the file 'data.txt' containing base64-encoded data.
### What I thought and executed:
1. Since the suggested commands for this level matched the previous levels' pattern of running `man` first, I knew the `base64` command was to be used.
2. I ran `base64 data.txt`, which was the wrong move, as this command is for encoding data, and the data in 'data.txt' was already encoded using base64 — so it took me some time to figure out the command for decoding it.
3. I ran `base64 -d data.txt`, which decodes the file, giving me the password for the next level.
### What was required:
|Commands required (in order) | Purpose                                        |
|-----------------------------|---------------------------------------------------|
| `base64 -d data.txt`        |To decode the data encoded in the file 'data.txt' |
### What I learnt:
- '-d' is for 'decoding'; running the command without '-d' encodes the file further.

---

# Level 11 → 12
### Objective: Find the password for level 12 stored in file 'data.txt' where all lowercase letters (a-z) and uppercase letters (A-Z) have been rotated by 13 positions.
### What I thought and executed:
1. I had very little idea of what the objective meant, so I went to the 'Helpful Reading Material' link on ROT13 on Wikipedia.
2. I found that ROT13 is a well-known cypher used in the past which rotates each selected character in (a-z) and (A-Z) by 13 letters in the forward direction.
3. I figured you have to `cat` this file and then rotate the letters by 13, so I used the `tr` command, used to 'translate, delete and squeeze' characters, which alters characters based on a mapping.
4. This was the first level where I had no idea of the syntax and googled it. You pipeline from `cat` to `tr` to do ROT13.
5. I ran `cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'` where `cat` reads the file 'data.txt', and this output is given to `tr` as input. `tr` maps 'A-Za-z' (A-Z and a-z) to 'N-ZA-Mn-za-m' (Z is replaced by N... wrapping through the alphabet by 13 positions).
### What was required:
|Commands Required (in order)                 |Purpose                                                      |
|---------------------------------------------|-----------------------------------------------------------------|
|`ls`                                         |To make sure file 'data.txt' exists in the home directory        |
|`cat data.txt \| tr 'A-Za-z' 'N-ZA-Mn-za-m'` |To rotate the characters of file 'data.txt' by 13 characters |
---

# Level 12 → 13
### Objective: Find the password for level 13 in a file 'data.txt' which is a hexdump of files repeatedly compressed.
### What I thought and executed:
1. On the official site: [OverTheWire Bandit](https://overthewire.org/wargames/bandit/), it is suggested to make a temporary directory and work there so as not to damage the file, and to read the `man` pages of the suggested commands I didn't already know (`mkdir`, `cp`, `mv`).
2. I ran `mktemp -d`, which makes a temporary directory in which I can work and decompress a copy of the file 'data.txt' without harming the original file.
3. Then it gives you an address for the directory (in my case: /tmp/tmp.BlJKXiMlnx).
4. Then I ran `cp ~/data.txt /tmp/tmp.BlJKXiMlnx` to copy the file 'data.txt' to the temporary directory I made earlier.
5. Then I ran `cd /tmp/tmp.BlJKXiMlnx` to switch to the temporary directory from the home directory.
6. I ran `ls` to confirm whether the file 'data.txt' had been copied.
7. I ran `xxd -r data.txt > data`, to reverse the hexdump on the file 'data.txt' into a new file 'data' — the same content, but as raw bytes instead of a hexdump.
8. I ran `ls` to see the file 'data' and `file data` to see how it has been compressed.
9. It was gzip compressed. To decompress it, I needed the file to have the extension '.gz', so I used `mv data data.gz`, which renamed the file 'data' with the extension '.gz'.
10. `mv` mainly works with the syntax `mv [options] source destination`; if the destination doesn't exist (or is left blank), then the file is renamed.
11. I ran `gzip -d data.gz` to decompress the file 'data.gz' where '-d' is for decompress.
12. I ran `file data` to check which compression was on the file now (as the instructions on [OverTheWire Bandit](https://overthewire.org/wargames/bandit/) mention that the file has been *repeatedly* compressed, so multiple decompressions were needed, including `tar`, `gzip` and `bzip2`).
13. It was bzip2 compressed. So the file 'data' had to be renamed to 'data.bz2' (with the '.bz2' extension for decompression). I ran `mv data data.bz2` followed by `bzip2 -d data.bz2` to decompress ('-d') the file. I ran `file data` again to see the next decompression to be made. These steps had to be repeated until the file type showed *ASCII*, i.e. plain text readable by humans.
14. It was gzip compression again, so the same steps were followed. After running `file` on the newly decompressed file, it was `tar` compressed, which has a few different steps.
15. This is because, unlike gzip or bzip2, which compress single files, `tar` bundles multiple files into 1 archive (like a zip folder), so after decompression, `ls` also had to be run to check which files had been extracted.
16. I ran `mv data data.tar` and `tar -xf data.tar` to decompress the files. Here, in '-xf', '-x' is for *extract*, telling the system to extract the files from the archive and load them onto my system. The 'f' specifies the archive name that is to be extracted.
17. I ran `ls` and got the file 'data5.bin'. Then `file data5.bin` to find further `tar` compression on it. I decompressed it, ran `ls` on data5.tar, and got a file 'data6.bin' which was gzip compressed — same decompression steps followed.
18. On decompression of 'data6.bin' I obtained 'data8.bin' which was gzip compressed; on its decompression, `file data8` showed this was an *ASCII* file. I ran `cat data8` and obtained the password for the next level.
### What was required:
|Commands Required (in order)       |Purpose                                                                                  |
|-----------------------------------|--------------------------------------------------------------------------------------------|
|`mktemp -d`                        |To make a unique temporary directory                                                               |
|`cp ~/data.txt /tmp/tmp.BlJKXiMlnx`|To copy the file 'data.txt' into the newly made directory of the address '/tmp/tmp.BlJKXiMlnx'|
|`cd /tmp/tmp.BlJKXiMlnx`           |To switch directories                                                                    |
|`xxd -r data.txt > data`           |To reverse the hexdump on 'data.txt' into a new file 'data'                               |
|`file data`                        |To check the type of compression on 'data'                                               |

Process to decompress `gzip` compression:

|Commands Required (in order)       |Purpose|
|-----------------------------------|-------|
|`mv data data.gz`                  |To rename the file 'data' to 'data.gz' to decompress the gzip compression                |
|`gzip -d data.gz`                  |To decompress the file 'data.gz'                                                         |
|`file data`                        |To check the next decompression on file 'data'                                           |

Process to decompress `bzip2` compression:

|Commands Required (in order)|Purpose|
|----------------------------|-------|
|`mv data data.bz2`                 |To rename the file 'data' to 'data.bz2' to decompress the bzip2 compression              |
|`bzip2 -d data.bz2`                |To decompress the file 'data.bz2'                                                        |
|`file data`                        |To check the next decompression                                                           |

Process to decompress `tar` compression:

|Commands Required (in order)|Purpose|
|----------------------------|-------|
|`mv data data.tar`                 |To rename the file 'data' to 'data.tar' to decompress the tar compression                |
|`tar -xf data.tar`                 |To decompress the archive data                                                           |
|`ls`                               |To check the decompressed files from the 'data' archive                                  |
|`file data5.bin`                   |Checking the type of the file obtained from the archive                                  |

.
.   (This process of decompression for `gzip`, `bzip2`, `tar` is repeated until an ASCII-type file is obtained.)
.
.

|Commands Required (in order)|Purpose|
|----------------------------|-------|
|`mv data8.bin data8.gz`            |To rename file 'data8.bin' to 'data8.gz' to decompress the gzip compression              |
|`gzip -d data8.gz`                 |To decompress the gzip compression                                                        |
|`file data8`                       |To check the file type of file 'data8'                                                        |
|`cat data8`                        |To read the content of the ASCII file (human-readable file)                                  |
### What I learnt:
- To decompress gzip, bzip2 and tar, the extensions '.gz', '.bz2' and '.tar' respectively are required on the files.
- `tar` compresses multiple files to form an archive, whereas gzip and bzip2 compress single files.
---

# Level 13 → 14
### Objective: To find the private SSH key stored in '/etc/bandit_pass/bandit14', only accessible by user bandit14
### What I thought and executed:
1. I ran the `ls` command to check which files are in the directory. I ran `cat HELP` and `cat sshkey.private`. Access denied for `cat sshkey.private`.
2. I ran `cat /etc/bandit_pass/bandit14` but access was denied again. I realised access is only for user bandit14.
3. I read about SSH/OpenSSH/keys in the 'Helpful Reading Material' section on the official website [OverTheWire Bandit](https://overthewire.org/wargames/bandit/).
4. I ran `scp -P 2220 bandit13@bandit.labs.overthewire.org:~/sshkey.private .`. `scp` is the Secure Copy Protocol, which safely transfers files and directories between different systems over a network. This command translates to 'on that server, logged in as bandit13, grab the file sshkey.private from the home directory'. The '.' at the end copies the file to my current directory on my local machine.
5. I ran `exit` to exit the bandit13 session. Then on my local machine/VM I ran `ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220` where 'ssh' is the secure shell command, '-i sshkey.private' is used as my private key instead of the usual password, 'bandit14' is the user, 'bandit.labs.overthewire.org' is the remote server, and '-p 2220' is the port for bandit rather than the standard port 22 for `ssh` commands.
6. I ran into an error because the permissions on ' sshkey. private ' (0640) were too open. For a private key, it should have permissions that restrict usage to the owner only, so the `chmod` command is used.
7. I ran `chmod 600 sshkey.private` (which should have been run before the ssh command), where `chmod` is the command used, '6' is 'rw' i.e. only the owner can read and write, '0' is 'group gets nothing', and the last '0' is 'others get nothing'.
8. Then I ran the ssh command again and obtained the password for level 14, which can be entered when trying to log into bandit14 directly from the outside.
### What was required:
|Commands Required (in order)                                         |Purpose                                                    |
|---------------------------------------------------------------------|----------------------------------------------------------------|
|`ls`                                                                 |To list all files in the home directory                        |
|`cat HINT`                                                           |To get an idea of what should be done at this level        |
|`scp -P 2220 bandit13@bandit.labs.overthewire.org:~/sshkey.private .`|To securely copy the file 'sshkey.private' to the local machine|
|`chmod 600 sshkey.private`                                           |To change the permissions of the file to match those of a private key|
|`ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220`|To SSH into the server using sshkey.private instead of a password|
### What I learnt:
- All passwords for the current levels (say L) are stored in files '/etc/bandit_pass/banditL' and can be accessed only by the user banditL.
- Ports are like doors to the server building. Specific ports are for specific protocols, like:
    - port 22: default for SSH
    - port 80: HTTP
    - port 443: HTTPS
    - port 2220: bandit's custom SSH port
- Private keys have restricted permissions, and SSH refuses to use private keys that are accessible beyond the owner.
---

# Level 14 → 15
### Objective: To retrieve the password by submitting the password of the current level to port 30000 on localhost
### What I thought and executed:
1. I ran `man` on the suggested commands (`ssh`, `telnet`, `nc`, `openssl`, `s_client` and `nmap`) and figured `nc` (netcat) was the way to go, as it's used as a raw pipe between 2 machines over a network without any encryption.
2. I ran `nc localhost 30000`, where 'localhost' is the machine to connect to and '30000' is the port.
3. It requested the password of the current level and returned the password for the next level as output.
### What was required:
|Commands Required (in order)|Purpose                                           |
|----------------------------|------------------------------------------------------|
|`nc localhost 30000`        |To connect to the 'localhost' machine via port 30000|
### What I learnt:
- `nc` is used to connect 2 machines on a network directly, without encryption.
---

# Level 15 → 16
### Objective: To retrieve the password for the next level by submitting the password of the current level to port 31000 on localhost using SSL/TLS encryption
### What I thought and executed:
1. I ran `man openssl` and figured the `openssl s_client` command was to be used, as `s_client` is like `nc` but wrapped with SSL/TLS encryption. It opens a connection between host and port while letting us type and send data.
2. I ran `openssl s_client -connect localhost:31000`, where 'openssl' is the main command, 's_client' is the sub-command, '-connect' is the flag, 'localhost' is the host machine, ':' is the separator and '31000' is the port.
3. It waits for me to enter the password of the current level as input and gives the password of the next level as output.
### What was required:
|Commands Required (in order)               |Purpose                                                 |
|-------------------------------------------|------------------------------------------------------------|
|`openssl s_client -connect localhost:31000`|To establish a connection between localhost and port 31000|
### What I learnt:
- `s_client` and `nc` differ only in the sense that one encrypts data with SSL/TLS while the other simply connects host and port without encryption.
---

# Level 16 → 17
### Objective: To retrieve the password for the next level by submitting the password of the current level to a listening port that speaks SSL/TLS in the range 31000-32000
### What I thought and executed:
1. A 'listening port' is an active port waiting for a connection. It's like a door behind which someone is waiting to answer.
2. I was effectively looking for a 'port scanner'.
3. The `nmap` command is a port scanner, so I ran `nmap -p 31000-32000 localhost`, where 'nmap' is the command, '-p 31000-32000' is the port range and 'localhost' is the machine being scanned. It showed all the listening ports (in my case, 5: 31046, 31518, 31691, 31790 and 31960).
4. To check if they speak SSL/TLS, I ran the command `openssl s_client -connect localhost:port -ign_eof`. All but 2 ports (31518 and 31790) showed no result or simply echoed back the password of the current level I entered.
5. Before adding '-ign_eof', the system thought that right after passing the data on standard input, it was 'end of communication' and would automatically close the connection. '-ign_eof' stands for 'ignore end of file', which allows the system to pause after sending all required data, allowing me to comfortably enter the password for this level, or use the 'k' command when it read KEYUPDATE. The 'k' command continues the system as-is and expects further output too.
6. On port '31790' I got a passkey for the next level.
7. I googled this part, as to what to do with the passkey, because unlike level 13 → 14 where the passkey was already stored in a file, I had to make a file here and then move forward.
8. I copied the entire passkey (from the '---BEGIN...' line to the '---END...' line) using Ctrl+C after selecting all of it. I ran `exit` to exit the bandit terminal.
9. I ran `nano bandit17.key`, where 'nano' is a simple text editor that works in the terminal. On entering this, I pasted the passkey with Ctrl+V, then exited with Ctrl+X, 'yes' and 'continue'.
10. Then I ran `chmod 600 bandit17.key` to change its permissions, making it fit for use as a private key by SSH.
11. I ran `ssh -i bandit17.key bandit17@bandit.labs.overthewire.org -p 2220`.
12. Once in the bandit17 server, I ran `cat /etc/bandit_pass/bandit17` to store the password of level 17 so that I could use it to log into the level externally via the normal SSH command.
### What was required:
|Commands Required (in order)|Purpose|
|----------------------------|-------|
|`nmap -p 31000-32000 localhost`|To scan for the listening ports|
|`openssl s_client -connect localhost:31790 -ign_eof`|To check SSL/TLS on the listening ports|
|`copy passkey`|To store it|
|`exit`|To exit the terminal|
|`nano bandit17.key`|To make a file bandit17.key, paste the passkey into it, Ctrl+X to exit|
|`chmod 600 bandit17.key`|To make it fit for use as a private key by SSH|
|`ssh -i bandit17.key bandit17@bandit.labs.overthewire.org -p 2220`|To SSH into level 17 via private key rather than a password|
|`cat /etc/bandit_pass/bandit17`|To store the actual password for level 17 for logging in externally via SSH|
### What I learnt:
- The password for a level (say 17) is always stored in the file '/etc/bandit_pass/bandit17'.
- `nano` is a simple text editor that works through the terminal.
---

# Level 17 → 18
### Objective: To find the password for the next level, which is the only different line in file 'passwords.new' compared to file 'passwords.old', both stored in the home directory
### What I thought and executed:
1. I ran `man diff` from the suggested commands on the official site [OverTheWire Bandit](https://overthewire.org/wargames/bandit/). This command (without any specific options) shows the difference in file2 relative to file1 when executed as `diff file1 file2`.
### What was required:
|Commands Required (in order)      |Purpose                                                               |
|----------------------------------|--------------------------------------------------------------------------|
|`diff passwords.old passwords.new`|To identify the different lines between 'passwords.old' and 'passwords.new'|
---

# Level 18 → 19
### Objective: To find the password for the next level stored in a file 'readme' in the home directory, on a level that's been hacked to log out as soon as you log in.
### What I thought and executed:
1. On simply trying to run `ssh`, `.bashrc` runs immediately after the full shell is launched and logs me out of bandit18 — hence 'bye bye!'.
2. So I needed to run `cat readme` as soon as I was on the server, rather than waiting for the full shell to load.
3. I googled how to do this and ran the command `ssh bandit18@bandit.labs.overthewire.org -p 2220 "cat readme"`. The command inside "" runs immediately on the server.
### What was required:
|Commands Required (in order)|Purpose|
|----------------------------|-------|
|`ssh bandit18@bandit.labs.overthewire.org -p 2220 "cat readme"`|To run the `cat readme` command immediately after `ssh` without waiting for the full shell to load|
### What I learnt:
- The command in "" runs immediately by bypassing the interactive login shell.
---

# Level 19 → 20
### Objective: To find the password in '/etc/bandit_pass/bandit20' after correctly executing the setuid binary command in the home directory
### What I thought and executed:
1. I ran `ls` and found an executable file — a file that can be run as an individual program.
2. I ran `./bandit20-do` where `./` means run this file from the current directory.
3. I read about 'setuid' on Wikipedia as suggested in 'Helpful Reading Material'.
4. I ran `./bandit20-do whoami` as suggested in the terminal output.
5. This command gives me access to files that only bandit20 has access to, i.e. via `cat /etc/bandit_pass/bandit20`.
6. So I ran `./bandit20-do cat /etc/bandit_pass/bandit20` to use the `cat` command while having the access of 'bandit20' via the executable file 'bandit20-do'.
7. These 2 commands don't work separately, i.e. running `./bandit20-do` alone and then `cat /etc/bandit_pass/bandit20` separately, since when we execute `cat` separately, we execute it as the 'bandit19' user, who doesn't have access to '/etc/bandit_pass/bandit20'.
### What was required:
|Commands Required (in order)                 |Purpose                                                         |
|---------------------------------------------|----------------------------------------------------------------|
|`ls`                                         |To know which files are in the home directory                   |
|`./bandit20-do`                              |To execute the executable file 'bandit20-do'                    |
|`./bandit20-do whoami`                       |As suggested in the terminal output                             |
|`./bandit20-do cat /etc/bandit_pass/bandit20`|To access the password for level 20 with access to bandit20|
### What I learnt:
- To execute an executable file named 'file', run `./file`, i.e. 'execute the file "file" in this directory'.
---

# Level 20 → 21
### Objective: To receive the password from a setuid binary after correctly executing it
### What I thought and executed:
1. I ran `ls` to check the name of the executable setuid binary file in the home directory — it was 'suconnect'.
2. I ran `./suconnect` to see how the command worked.
3. I ran `./suconnect password_of_level_20`, which failed, as this was the wrong syntax for executing this command.
4. 'suconnect' reads a password sent to a listening port; if it matched the password for level 20, it would give the password for level 21 in its output.
5. I ran `echo "0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO" | nc -l -p 1234` where `echo` prints whatever is entered in the "". The '|' (pipeline) sends '0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO', i.e. the password for level 20, as input for the `nc` command.
6. `nc` (netcat) is the simplest way to open a port on the localhost machine and send data to whatever is connected. '-l' is for 'listen for incoming connections' and '-p' (lowercase) is for the source port.
7. Then I ran `./suconnect 1234`. This was the wrong move — both these commands had to be run simultaneously. An analogy for this could be: `./suconnect` dials a phone call, `nc` picks up and speaks the password on port '1234'. These commands need to be run together as a process rather than as successive commands.
8. There are 2 ways to do this:
    - Use the `tmux` command, which creates multiple terminal panes, so both commands can be run at the same time in different panes.
      |Commands I ran for the `tmux` approach|Purpose|
      |----------------------------------|-------|
      |`tmux`|To start 'tmux'|
      |Ctrl+b|To split into 2 panes|
      |`echo "0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO" \| nc -l -p 1234`| To be run in the top pane, sending the password of the previous level to port 1234|
      |Ctrl+b then arrow down|To switch to the bottom pane|
      |`./suconnect 1234`|To read the password of the previous level from port 1234|
    - *shortcut*: `echo "0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO" \| nc -l -p 1234 & ./suconnect 1234` to run both commands at the same time — however this gave an error, as `suconnect` was faster than `echo`/`nc` and didn't find anything at port 1234, so it failed. I then ran
    `echo "0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO" \| nc -l -p 1234 & sleep 1 && ./suconnect 1234`, allowing the system to pause for 1 second before letting `suconnect` read the password from port 1234.
9. I went with the shortcut method for this one.
### What was required:
|Commands Required (in order)                                                            |Purpose|
|----------------------------------------------------------------------------------------|-------|
|`ls` |To know the names of the files to be used                                          |
|`./suconnect`|To see what the 'suconnect' command did                                  |
|`echo "0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO" \| nc -l -p 1234 & sleep 1 && ./suconnect 1234`|To read the password of the previous level from a listening port|
### What I learnt:
- In the syntax shown on `man` pages, things written in [ ] don't actually need to be entered in the terminal — the brackets themselves are just notation.
- `echo` is a basic Linux command that prints text or characters written in " ".
- `nc`/'netcat' is the simplest command to open a port on localhost and send data to whatever it's connected to.
- This level was a basic introduction to TCP client/server interaction.
- `&` runs a command in the background so the next command can start without waiting for it, and `&&` runs the next command only if the previous one succeeds.
- `sleep 1` pauses the system for 1 second before executing the command to its right.
---

# Level 21 → 22
### Objective: To find the password for the next level by looking into '/etc/cron.d/' as a background process runs at intervals.
### What I thought and executed:
1. I ran `man cron` and came across the word 'daemon', which means a background process that runs independently of the user interface, performing tasks for the system.
2. Then I ran `cat /etc/cron.d/`, which told me this was a directory.
3. Since it's a directory, I ran `cd /etc/cron.d/` to switch into it.
4. I ran `ls` to check the contents of this directory.
5. I ran `cat cronjob_bandit22` among all the other files (notably, 2 for levels 23 and 24, and a few for other wargames).
6. In the output, a pattern '* * * * *' appeared, which meant 'running every minute'. So I ran `cat /usr/bin/cronjob_bandit22.sh`.
7. Initially I thought the hash it displayed was the password, so I quickly saved it, exited, and tried to SSH into level 23, only to realise while entering the password that it was wrong. After trying 5 times, I went back to the terminal output and realised I had to `cat` a different file whose address was printed in that output.
8. To do that, I had to run all the commands again to re-enter the directory '/etc/cron.d/'.
9. Then I ran `cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv`, which revealed the actual password for level 23.
### What was required:
|Commands required (in order)               |Purpose                                                  |
|-------------------------------------------|-----------------------------------------------------------|
|`cat /etc/cron.d/`                         |In an attempt to read '/etc/cron.d/'                       |
|`cd /etc/cron.d/`                          |To switch directories                                    |
|`ls`                                       |To check the contents of the new directory               |
|`cat cronjob_bandit22`                     |To read the relevant file for this level                 |
|`cat /usr/bin/cronjob_bandit22.sh`         |To follow the instructions in the terminal output          |
|`cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv`| To read the file address returned in the terminal output|
### What I learnt:
- ALWAYS read the terminal output and follow its guidance.
---

# Level 22 → 23
### Objective: To find the password for the next level by looking into '/etc/cron.d/' as a background process runs at intervals.
### What I thought and executed:
1. I ran `cat /etc/cron.d/` — it turned out to be a directory again.
2. I ran `cd /etc/cron.d/` to switch directories.
3. I ran `ls` to check the contents of the new directory.
4. I ran `cat cronjob_bandit23` to read the relevant file for this level.
5. I ran the commands shown in the terminal output word for word:
    myname=$whoami
    mytarget=$(echo I am user $myname |md5sum | cut -d - - -f 1)
    echo "/etc/bandit_pass/$myname to /tmp/$mytarget
    cat /tmp/$mytarget
which was the **wrong** move, as it took 'whoami' to be bandit22 by default, so it just returned the password of the current level.
6. After realising my mistake, I ran `echo "I am user bandit23" | md5sum | cut -d ' ' -f 1`, which returned a hash.
7. Then, before assuming these characters were my password, I ran `cat /tmp/8ca319486bfbbc3663ea0fbe81326349` and got the correct password for the next level.
### What was required:
|Commands Required (in order)                           |Purpose                                  |
|-------------------------------------------------------|----------------------------------------------|
|`cat /etc/cron.d/`                                     |In an attempt to read '/etc/cron.d/'       |
|`cd /etc/cron.d/`                                      |To switch directories                    |
|`ls`                                                   |To read the contents of the new directory|
|`cat cronjob_bandit23`                                 |To read the relevant file for this level |
|`echo "I am user bandit23" \| md5sum\| cut -d ' ' -f 1`|To generate the target hash filename                                          |
|`cat /tmp/8ca319486bfbbc3663ea0fbe81326349`            |To read the password from the resulting file                                         |
---

# Level 23 → 24
### Objective: To find the password for the next level by looking into '/etc/cron.d/' and following through with what is being executed
### What I thought and executed:
1. I ran `cd /etc/cron.d/` to enter this directory.
2. I ran `ls` to see the different files in this directory.
3. I ran `cat cronjob_bandit24`, the relevant file for level 24.
4. I ran `cat /usr/bin/cronjob_bandit24.sh` to read the content of this file.
5. Unlike previous levels, this level required a fake directory to be made (as suggested on [OverTheWire: Bandit](https://overthewire.org/wargames/bandit/)), so I ran `mkdir /tmp/mydir` to create a temporary directory 'mydir' in the tmp folder.
6. `cronjob` was going to run its procedure every minute as user 'bandit24'. It read the contents of the file at the specified address ('/var/spool/bandit24/foo/' as stated in the terminal output) and executed it if it was an executable file.
7. As it runs files with the permissions of user 'bandit24', it has permission to execute `cat /etc/bandit_pass/bandit24`. So the goal is to make a file containing this command, store it in the specified location, and set its permissions to 777, i.e. giving the owner, owner's group, and others the permissions 'rwx' — read, write and execute. (777 in binary is 111, so all permissions 'read', 'write' and 'execute' are turned 'on' with 1.)
8. I ran `nano /tmp/mydir/myscript.sh` to create a text file in the 'mydir' directory. It opened a simple text editor in the terminal, where I typed '#!/bin/bash' on line 1 and `cat /etc/bandit_pass/bandit24 > /tmp/mydir/password` on line 2, where '>' sends the output of the first command to the *file* at the address '/tmp/mydir/password' instead of the terminal.
9. I ran `chmod +x /tmp/mydir/myscript.sh` to make the file 'myscript.sh' executable. If this file weren't executable, it would just be a text file that `cronjob` would refuse to run, serving no purpose.
10. I ran `chmod 777 /tmp/mydir` to change the permissions of the directory to '777' as explained in point 7.
11. I ran `cp /tmp/mydir/myscript.sh /var/spool/bandit24/foo/` to copy the file 'myscript.sh' to the specified location. It's necessary to copy an external file to that location instead of creating everything there directly, since `cat /usr/bin/cronjob_bandit24.sh` shows it will execute and *delete* the files every minute — so we'd lose the file at that location. Having the command store the password in an external file lets us access the content even after the original is deleted.
12. Since `cronjob` runs its procedure of reading and then deleting files at that location every minute, I waited 60 seconds before running `cat /tmp/mydir/password` to read the password `cronjob` had stored there.
### What was required:
|Commands Required (in order)|Purpose|
|----------------------------|-------|
|`cd /etc/cron.d/`|To switch directories|
|`ls` |To look at the different files listed in the directory|
|`cat cronjob_bandit24`|To read the most relevant file for this level|
|`cat /usr/bin/cronjob_bandit24.sh`|To read the stored script file|
|`mkdir /tmp/mydir`|To make a temporary directory|
|`nano /tmp/mydir/myscript.sh`|To make a file 'myscript.sh' in the new directory|
|`#!/bin/bash` on line 1; `cat /etc/bandit_pass/bandit24 > /tmp/mydir/password` on line 2||
|`chmod +x /tmp/mydir/myscript.sh`|To make the file executable|
|`chmod 777 /tmp/mydir`|To change the permissions of the directory to make it accessible and writable by everyone|
|`cp /tmp/mydir/myscript.sh /var/spool/bandit24/foo/`|To copy the file to the desired location|
|`cat /tmp/mydir/password`|To be run **1 minute AFTER** the previous command, to read the password for the next level from the file 'password'|
### What I learnt:
- Permissions in Linux are split into 3 groups: 'owner', 'owner's group' and 'others' ('others' means everyone else besides owner and group). There are 3 permissions: 'read', 'write' and 'execute'.
- 777 in binary is 111, which means the permissions 'rwx' (read, write and execute) are given to all 3: owner, owner's group and others.
- `mkdir` allows you to make your own directory at a desired location.
- The `+x` option in `chmod` makes the selected file executable.
- '>' redirects, i.e. sends the output of the first command to another *file* whose address is given after it.
  '|' (pipeline) sends the output of the first command to another *command* written after it.
---

# Level 24 → 25
### Objective: To retrieve the password for the next level as output obtained after entering the password of the current level, along with a specific numeric 4-digit pincode, to port 30002
### What I thought and executed:
1. I first tried `echo "gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8" | nc localhost 30002` (without the 4-digit secret pincode) to see the output type. It was interactive, asking for a 4-digit pincode I did not know at that point.
2. I had two choices:
    - Manually enter all possible 4-digit numeric pincodes from 0000 to 9999, i.e. brute force.
    - In a Nano file, use a loop with `nc`, piping the results of the loop (a pincode from 0000 to 9999) to port 30002 using `nc localhost 30002`.
    The second method is shorter, more efficient and works best for larger search spaces.
3. The file also had to be made executable using `chmod +x file_address_and_name` so the shell could execute the loop and generate all possible 4-digit pincodes.
4. I googled the syntax for the loop. I ran `nano /tmp/bruteforce.sh` to create a file called 'bruteforce.sh'.
   In the file I typed:
```
#!/bin/bash
    for i in $(seq -w 0000 9999); do
        echo "gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8 $i"
    done | nc localhost 30002
```
5. Then I pressed `ctrl+x` to close the file, `yes` and `enter`.
6. I ran `chmod +x /tmp/bruteforce.sh` to make the file 'bruteforce.sh' executable.
7. I ran `/tmp/bruteforce.sh` to execute this file. In the terminal output, 'wrong' printed continuously until the correct 4-digit pincode was found, at which point it displayed the password for the next level.
### What was required:
|Commands Required (in order) |Purpose        |
|-----------------------------|------------------------------------------------------------------|
|`nano /tmp/bruteforce.sh`|To create the file 'bruteforce.sh' and enter the required loop, as discussed in point 4 above|
|`chmod +x /tmp/bruteforce.sh`|To make the file executable|
|`/tmp/bruteforce.sh`|To execute the executable file 'bruteforce.sh'   |
### What I learnt:
- The extension on file 'bruteforce.sh', i.e. '.sh', is just for humans, so at a glance we know it's a shell script. For the system, the shebang line `#!/bin/bash` at the top of the file tells it this is a shell script.
- '/tmp' is the temporary directory in Linux that stores temporary files.
---

# Level 25 → 26
### Objective: To use a passkey to connect to the next level, but the shell for user bandit26 isn't `/bin/bash`
### What I thought and executed:
1. I ran `man more`, then `ls` and `more bandit26.sshkey`. There's a small but crucial difference between `more`, `less` and `cat` (discussed in 'What I learnt' below).
2. I ran `cat /etc/shells` to check the available valid login shells. `more` was being used.
3. I ran `cat bandit26.sshkey`, copied the entire content, and exited bandit25 back to my local machine.
4. Then I ran `nano bandit26.sshkey`, pasted the copied content, and closed with `ctrl+x`.
5. I ran `chmod 600 bandit26.sshkey` to set permissions matching a private SSH key file.
6. From my local machine, I ran `ssh -i bandit26.sshkey bandit26@bandit.labs.overthewire.org -p 2220` with the terminal shrunk to 1-2 lines.
7. If the command is entered without shrinking the terminal window size, `more` doesn't stop for keyboard input, and the shell is set up so it immediately kicks us out after loading bandit26.
8. Something like `more(15%)` should show up. Then I typed `v` to open the `vi` editor (an editor similar to `nano`).
9. In `vi` I typed `:set shell=/bin/bash` to change the shell to a normal bash shell, and pressed enter.
10. To activate it, I typed `:shell` and pressed enter. Now the shell type is bash (`more` also changes to green and shows `--More--`).
11. Now I'm in bandit26. To get the password for the current level, I ran `cat /etc/bandit_pass/bandit26`.
### What was required:
|Commands (in order)|Purpose|
|-------------------|-------|
|`ls`|To list the files in the home directory|
|`cat bandit26.sshkey`|To read the file bandit26.sshkey, copy its entire content, and exit back to the local machine|
|`nano bandit26.sshkey`|To make the file bandit26.sshkey, paste the copied content, and exit with `ctrl+x`|
|`chmod 600 bandit26.sshkey`|To change the permissions of the file to that of a private SSH key file|
|`ssh -i bandit26.sshkey bandit26@bandit.labs.overthewire.org -p 2220`|To SSH into the next level via the private key, with the terminal window shrunk to 1-2 lines|
|`v`|To enter the `vi` editor|
|`:set shell=/bin/bash`|To change the shell type to bash|
|`:shell`|To activate the above change|
|`cat /etc/bandit_pass/bandit26`|To read the password for the current level|
### What I learnt:
- |`cat`|`more`|`less`|
  |-----|------|------|
  |Dumps everything at once (even 1000 lines); the user's screen stops at the end of the document|Displays 1 screenful of content, waits for us to read, then presses `space` to continue|*`less` is 'more' but better* — you can scroll up and down, search with `/`, and quit with `q`|
- `vi` is another terminal-based text editor, like `nano`.
---

# Level 26 → 27
### Objective: To grab the password for level 27 after entering the shell from level 25
### What I thought and executed:
1. I ran `ls`.
2. I ran `cat bandit27-do`. Reading the output, I found that using `bandit27-do` gives me the access of bandit27, meaning I can easily read files that only bandit27 has access to while being bandit26.
3. I ran `./bandit27-do cat /etc/bandit_pass/bandit27` to read the password for the next level, with the access of level 27, via the file bandit27-do present in this directory (./).
### What was required:
|Commands Required (in order)|Purpose|
|----------------------------|-------|
|`ls`|To see which files are in the home directory|
|`cat bandit27-do`|To find out what this file does|
|`./bandit27-do cat /etc/bandit_pass/bandit27`|To read the password for level 27|
---

# Level 27 → 28
### Objective: To find the password for the next level by cloning a repository from a given URL and reading its content
### What I thought and executed:
1. I ran `sudo apt install git` to install git in the terminal.
2. I ran `git clone "ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo"` to clone the repo to my local machine.
3. I ran `ls` to see the cloned files.
4. I ran `cd repo` to switch into the 'repo' directory.
5. I ran `ls` to check the files in 'repo'.
6. I ran `cat README` to read the file 'README' and get the password.
### What was required:
|Commands Required (in order)|Purpose|
|----------------------------|-------|
|`sudo apt install git`|To install git on the terminal in the VM|
|`git clone "ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo"`|To clone the desired repo from the specified URL into the current directory|
|`ls`|To check the cloned files|
|`cd repo`|To switch into the cloned repository|
|`ls`|To check the list of files in the 'repo' directory|
|`cat README`|To read the file 'README'|
### What I learnt:
- **repository** = **directory** = **folder** (roughly, in this context)
---

# Level 28 → 29
### Objective: To find the password for the next level by cloning a repository from a given URL and reading its content
### What I thought and executed:
1. I ran `git clone "ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo"` to clone the required repo from the URL mentioned on the official site [OverTheWire: Bandit](https://overthewire.org/wargames/bandit/).
2. I ran `ls`, `cd repo`, and `cat README.md`.
3. It showed the password as 'xxxxxxx', i.e. redacted.
4. Git tracks changes made over time. The password was originally there, then someone made a commit updating it and redacting the password. So I needed to look at past commits, and ran `git log`.
5. It showed 3 commits, and I ran `git show <commit hash>` (commit hash written plainly, without the <>) to see the details of the suspicious commit (commit no. 2).
6. The password was revealed in that commit.
### What was required:
|Commands Required (in order)|Purpose|
|----------------------------|-------|
|`git clone "ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo"`|To clone the required repo onto the local machine|
|`cd repo`|To switch directories into 'repo'|
|`ls`|To check the files in 'repo'|
|`cat README.md`|To read the file 'README.md'|
|`git log`|To review past commits|
|`git show <>`|To check the details of a specified commit|
### What I learnt:
- When dealing with `git`, one of the 2 most important tools to use every time is `git log`.
- (Already mentioned, but relevant anyway) Ubuntu doesn't require extensions on filenames — that's only for humans to know at a glance what type of file it is. E.g. in 'README.md', the extension 'md' is for users to recognise it as a Markdown file; Ubuntu identifies the file type from its content.

# Level 29 → 30
### Objective: To obtain the password for the next level by cloning the required repository and reading its content
### What I thought and executed:
1. I ran `git clone "ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo"`.
2. I ran `cd repo`, `ls`, `cat README.md`. It said the password hadn't been decided yet.
3. I ran `git log` and `git show <>` on all suspicious commits, but got nothing.
4. I asked Claude about git, and besides `git log`, the second most important tool is `git branch -a`, which shows all other branches — some of which could still be unaltered and contain the password.
5. 'dev' is usually where the actual work is done before being cleaned up, so there was a high chance the password was still there. I ran `git checkout origin/dev`.
6. Now in the 'dev' branch, I ran `cat README.md` again and got the password.
### What was required:
|Command Required (in order)|Purpose|
|---------------------------|-------|
|`git clone "ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo"`|To clone the required repo from the given URL|
|`cd repo`|To switch directories|
|`cat README.md`|To read the file 'README.md'|
|`git branch -a`|To see other branches where the password might still be present|
|`git checkout origin/dev`|To switch to the 'dev' branch|
|`cat README.md`|To read the file 'README.md' while in the dev branch|
### What I learnt:
- The **2 most important** tools when dealing with `git` are **`git log`** and **`git branch -a`**.
---

# Level 30 → 31
### Objective: To find the password for the next level by cloning the required repo via git and reading its content
### What I thought and executed:
1. I ran `git clone "ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo"` along with `cd repo`, `ls`, `cat README.md`. The password was not there.
2. I ran the 2 trusted git tools, `git log` and `git branch -a`, but found nothing useful.
3. I ran `git tag` to see all added tags — another essential git tool.
4. Tags are labels attached to specific points in a repository that make working with a repo much easier.
5. It showed 'secret', so I ran `git show secret` and the password appeared.
### What was required:
|Commands Required (in order)|Purpose|
|----------------------------|-------|
|`git clone "ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo"`|To clone the repo|
|`cd repo`||
|`ls`||
|`cat README.md`||
|`git tag`|To see the names of all added tags in the repo|
|`git show secret`|To read the tag 'secret'|
### What I learnt:
- Along with `git log` and `git branch -a`, tags are also an important git feature for understanding the content of a repo.
---

# Level 31 → 32
### Objective: To find the password for the next level by cloning a repo from a given URL and reading its content
### What I thought and executed:
1. I ran `git clone "ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo"` along with `cd repo`, `ls`, `cat README.md`.
2. The README.md said to push a file to the repository to get the password.
3. So I ran `echo "May I come in?" > key.txt` to create the file key.txt with the content 'May I come in?' in one command.
4. `echo` prints the text in the "", and this time it was sent to a file 'key.txt' (if it existed already, the content would be appended; if not, a new file would be created) using '>'.
5. I ran `git add -f key.txt` to include this file in the next commit. The '-f' flag means **force** — without it, git would have ignored the .txt file, since a '.gitignore' file in that repo explicitly ignores .txt files by default.
6. I ran `git commit -m "add key"`, but it required configuration first, so I ran `git config --global user.email "a@a.com"` and `git config --global user.name "a"`, as the actual name/email didn't matter here.
7. I re-ran `git commit -m "add key"` and then `git push origin master`. The password was printed in the output along with a lot of extra text.
### What was required:
|Commands Required (in order)|Purpose|
|----------------------------|-------|
|`git clone "ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo"`|To clone the required repo|
|`cd repo`||
|`ls`||
|`cat README.md`||
|`echo "May I come in?" > key.txt`|To create the file key.txt and add its content in one command|
|`git add -f key.txt`|To include key.txt in the next commit; the '-f' flag forces inclusion of the ignored .txt file|
|`git commit -m "add key"`|To record the commit|
|`git config --global user.email "a@a.com"`|To set required configuration before committing|
|`git config --global user.name "a"`|To set required configuration before committing|
|`git commit -m "add key"`||
|`git push origin master`|To push the commits into the repo via the master branch|
### What I learnt:
- I could have made a new file 'key.txt' using `nano`, typed 'May I come in?', and it would have worked just as well. But `echo "May I come in?" > key.txt` does it in a single command.
---

# Level 32 → 33
### Objective: Find the password for the last level
### What I thought and executed:
1. After using `ssh` and the password for this level, the interface looked different. It wasn't a normal shell, as there was no `$` before keyboard input — instead there was `>`. The terminal introduction said this was an UPPERCASE Shell, where everything entered is automatically converted to uppercase.
2. This meant running `ls` wouldn't work, as the shell would interpret it as `LS`, which is nothing.
3. I had no prior knowledge of this, so I googled it and found that the variable `$0` isn't affected by this UPPERCASE Shell, as it's a special variable. Entering it into the terminal shifts the shell back to a normal one, as the `$` reappears.
4. I ran `whoami` and, surprisingly, it read bandit33. I asked Claude why this was the case.
5. UPPERCASE Shell is a setuid binary owned by bandit33. So on entering `$0`, we escaped the UPPERCASE Shell as a new shell expanded, inheriting the permissions of the UPPERCASE Shell.
6. We now had the permissions of the bandit33 user, so `cat /etc/bandit_pass/bandit33` was readable.
### What was required:
|Commands Required (in order)|Purpose|
|----------------------------|-------|
|`$0`|To return to a normal shell from the UPPERCASE Shell|
|`whoami`|To check the user of this newly spawned shell|
|`cat /etc/bandit_pass/bandit33`|To read the password of level 33|
### What I learnt:
- `$0` is a special variable (unaffected by the UPPERCASE Shell) that, when entered, expands into a new normal shell (with `$` at the start instead of `>`). In this process, the permissions of level 33 were also passed onto the newly made shell, as UPPERCASE Shell is a setuid binary belonging to level 33.
<<<<<<< HEAD
=======
---
# End of Levels!
>>>>>>> d7db06b04a31192b4b4015e7e21173d8bfa1d59b
---
# End of Levels!
---