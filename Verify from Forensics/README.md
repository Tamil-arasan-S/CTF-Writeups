Hello everyone,

This is my first write-up and it’s about the write-up for a CTF challenge in picoCTF that goes with the name Verify, a easy challenge.

<img width="1100" height="618" alt="1_OAssKbYJ_oUUhaznm1_hdg" src="https://github.com/user-attachments/assets/922ff390-9b75-4890-93f1-809fee2d4420" />

Challenge description:
People keep trying to trick my players with imitation flags. I want to make sure they get the real thing! I’m going to provide the SHA-256 hash and a decrypt script to help you know that my flags are legitimate.

My solution:
So at first after going through the description twice the problem was completely understood.

[Tip:Always understand the description by reading as many times as you can, it will solve most of the problem]

Basically we have to verify the hash that was provided in the checksum.txt with the files that was provided that contains almost 301 files.

<img width="1100" height="506" alt="1_gY9vI0AEjctCM09Y4oNNVw" src="https://github.com/user-attachments/assets/3b4fd259-3b17-4c7b-b516-a00a58149b92" />

The above image shows the checksum string that was SHA256.
Checksum is process that is used to for the integrity of the data that was communicated in the internet. We know that the hash can’t be decrypted until we a wordlist, so the hash file can be used as key to verify the integrity of a file. For an example if a data of [HACKER] was sent from person A to person B. If the person B needs to verify whether the data is not modified during the transmission, the Sender A can send the hash text to person B and verify that the data is not modified during the transmission.

[What if the hash file was also intercepted during the transmission😆😂🤣]

<img width="1100" height="187" alt="1_8-TxQHm8X-4rsYkELzH9fw" src="https://github.com/user-attachments/assets/d80a0afe-05fb-4d83-9a53-4c2f0ac3630b" />

<img width="1100" height="191" alt="1_v-qUwqTJ9PknrquYXb-rmw" src="https://github.com/user-attachments/assets/3a302846-612c-4e41-9a30-698adfd7c1c1" />

The command ls -1A | wc -l will count the count the number of files in a directory.

We can get the flag if we are able to get the SHA256 of the file directory and verify whether is there any file that maches the checksum.txt using the grep command.

<img width="1100" height="293" alt="1_CuXCgNjvvSRBv04uKaDKXg" src="https://github.com/user-attachments/assets/6ed7fa52-b3fa-45f3-b6f1-7189f62b29a7" />

<img width="1005" height="41" alt="1_j_9rPGaqF4Dm01Eub0xrtA" src="https://github.com/user-attachments/assets/ef7731ba-5d93-4516-af2c-da4c3ffde91a" />

So got to know that the file ****** is the file that has the correct hash value, so by running that we can the get the flag.


<img width="526" height="66" alt="1_bRe0y68CDMevonbYcXGgnA" src="https://github.com/user-attachments/assets/84b913c0-957a-413c-90a4-4732eb90d31e" />

So we got our flag🎉🎉🎉

Let me know in the comment whether you have any doubts.
