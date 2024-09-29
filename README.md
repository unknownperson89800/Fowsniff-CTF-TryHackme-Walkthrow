# TryHackMe: FowSniff

---

By: *UnknownPerson*

---

## Port Scanning: {22, 80, 110, 143}

From Port 80, we discovered the Gobuster directory `/security.txt`. Inside, we found the username `B1gN1nj4!`. A quick search on Google led us to a GitHub directory belonging to `B1gN1nj4!`, where we found leaked credentials that look like this:

```plaintext
mauer@fowsniff:8a28a94a588a95b80163709ab4313aa4
mustikka@fowsniff:ae1644dac5b77c0cf51e0d26ad6d7e56
tegel@fowsniff:1dc352435fecca338acfd4be10984009
baksteen@fowsniff:19f5af754c31f1e2651edde9250d69bb
seina@fowsniff:90dc16d47114aa13671c697fd506cf26
stone@fowsniff:a92b8a29ef1183192e3d35187e0cfabd
mursten@fowsniff:0e9588cb62f4b6f27e33d449e2ba0b3b
parede@fowsniff:4d6e42f56e127803285a0a7649b5ab11
sciana@fowsniff:f7fd98d380735e859f8b2ffbbede5a7e
Cracking the Passwords
We cracked these passwords using CrackStation. After testing them via brute force on the POP3 service with msfconsole, we obtained the following credential:

plaintext
Copy code
seina:scoobydoo2
Reading the Mail Server
Using the above credentials, we accessed the mail server and discovered SSH credentials:

plaintext
Copy code
baksteen:S1ck3n***ff+secure***ll
Privilege Escalation
After logging in with these SSH credentials, a banner was displayed upon login. Investigating further, we found a script at /opt/cube/cube.sh.

The script had both read and write permissions, which allowed us to inject a reverse shell listener. Since this script runs whenever someone logs in via SSH, we successfully gained root access.

Conclusion
Success! We have once again pawned a new machine.

Wow, Again We Pawnde New Machine