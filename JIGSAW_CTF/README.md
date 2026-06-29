# The forbidden door

<img width="573" height="582" alt="image" src="https://github.com/user-attachments/assets/7704dfe6-bff9-45cd-a2d9-5dc2394349e2" />

The description clearly says that out of 2500 endpoints, a particular one has the flag. If the burp suite prof. is avail, then we can perform the sniper attack ans filter for the `flag` keyword. But i performed this bruteforce by python automation script and the flag lies at /door/___ 

# The network nightmare

<img width="563" height="328" alt="image" src="https://github.com/user-attachments/assets/ab375e3e-fb9a-40e8-a72e-9f56b0978fff" />

This made me clueless at first, the login page was just a decoy and it does not validate our credentails at the backend.

<img width="675" height="172" alt="image" src="https://github.com/user-attachments/assets/cd8257ca-a78c-4c6f-bc93-762f1ff2ebfa" />

Then searced and common endpoints and in one of the endpoint there were some log files and at first i didn't notice that properly. Then later it had one of the major clue to get the RCE. There was a /ping endpoint and to access that there should be a non-standard HTTP request be present. And the log file gave that clue and then it was a simple RCE to get the flag.
