# HOW TO
Level02 shows a basic packet capture scenario and exploitation
## Tools
**Wireshark** (alternative: tcpdump): Wireshark is a packet capture tool, that has many, many features: from decoding to replaying packets, it's the number one tool when it comes to packet analysis

## Runthrought
When logging in the level02 account, we see a file called `level02.pcap`. I downloaded it using the `scp` command and used Wireshark to open it. To get a better grasp on the conversation, I right clicked a packet and clicked "Follow" and then "TCP Stream". It prompts us with a new window, containing the conversation between the two machines.
Here is the default content (note that wireshark adds colors to what was send by the client and what was sent by the server, but it can't be shown here):
```
..%..%..&..... ..#..'..$..&..... ..#..'..$.. .....#.....'........... .38400,38400....#.SodaCan:0....'..DISPLAY.SodaCan:0......xterm.........."........!........"..".....b........b....	B.
..............................1.......!.."......"......!..........."........"..".............	..
.....................
Linux 2.6.38-8-generic-pae (::ffff:10.1.1.2) (pts/10)

..wwwbugs login: l.le.ev.ve.el.lX.X
..
Password: ft_wandr...NDRel.L0L
.
..
Login incorrect
wwwbugs login: 
```
From there, I guessed that a user tryied to connect to a service using the login "levelX" and the password "ft_wandr...NDRel.L0L", and that the login failed.
So I tried to log in as "flag02" with password "ft_wandr...NDRel.L0L", but it wasn't working.
It took me some time, but I figured out that the text I was seeing was ASCII interpretation of the packets. Maybe it's UTF-8?
```
��%��%��&���� ��#��'��$��&���� ��#��'��$�� ����#����'��������  38400,38400����# SodaCan:0����'  DISPLAYSodaCan:0���� xterm��������"������!������"��"  b  b	B
���������� � 1������!��"����"����!������ ��"���� ��"��"����	�
������������
Linux 2.6.38-8-generic-pae (::ffff:10.1.1.2) (pts/10)

 wwwbugs login: l le ev ve el lX X
 
Password: ft_wandrNDRelL0L
 
 
Login incorrect
wwwbugs login: 
```
That's a lot clearer using UTF-8, we now have the password: "ft_wandrNDRelL0L"; I tried to connect to flag02 with it, and it worked.
