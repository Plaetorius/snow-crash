# HOW TO
Level00 is pretty straightforward. Upon looking at the intra video, you can see:
```
level00@bornToSec:~$ cat README
FIND this first file who can run only as flag00...
```
We now know that we are looking for a file that can only be run as flag00.
So we use find, the first command I tried was:
``find / -user flag00 2>/dev/null``
But I had forgotten the group, so I used the command:
``find / -user flag00 -group flag00 2>/dev/null``
Which leads to the file : ``/usr/sbin/john``, containing the text: ``cdiiddwpgswtgt`` which seems to be Ceasar code.
We use [DCode](https://www.dcode.fr/chiffre-cesar) to get the code, which is ``nottoohardhere``, the password for the ``flag00`` account.
