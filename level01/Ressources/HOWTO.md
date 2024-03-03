# HOW TO
Level01 is an intro on password hashing and storage, and John The Ripper 
## Tools
**John The Ripper** (alternative: Hashcat): JTR is a password cracking tool, that also allows to retrieve a password from a hash.

## Runthrought
There is no indication on where we should start to look. My first idea was then to look at the file `/etc/passwd`, which contains data about a user:
```
level01@SnowCrash:~$ cat /etc/passwd
...
flag00:x:3000:3000::/home/flag/flag00:/bin/bash
flag01:42hDRfypTqqnw:3001:3001::/home/flag/flag01:/bin/bash
flag02:x:3002:3002::/home/flag/flag02:/bin/bash
...
```
Each entry of the `/etc/passwd` file follows the model:
``name:PasswordHash:UserID:PrincipleGroup:Gecos:HomeDirectory:Shell``
I saw that the line for flag01 had a different password.
`x` means that the password is stored somewhere else, in `/etc/shadow`, a file only accessible by the root user; which is more secure, as everybody can have access to `/etc/passwd`.
I now have a password hash.
I create a `hash.txt` file, paste the hash: `flag01:42hDRfypTqqnw` and run `jtr hash.txt` and `jtr --show hash.txt`. The first command will crack the password with the default wordlist, and the second display the found password.
I get:
```
bash-3.2$john --show hash.txt
flag01:abcdefg
```
Giving us the password, `abcdefg`, and I can now get the flag
