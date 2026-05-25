You can access the room at : https://tryhackme.com/room/digdug
<img width="818" height="184" alt="1_MCbMZe2d7kOOsuJVwpYYOw" src="https://github.com/user-attachments/assets/d41c14d4-db92-46a9-983d-d59aa043d550" />
<img width="1100" height="553" alt="1_ITcTa2m9cR4Vj9Ev8eJMzA" src="https://github.com/user-attachments/assets/54dd1028-7c95-4834-9203-4bac1f8fd970" />

So the Challenge hint suggests that the Concept of DNS is involved here and we’ll have a brief information about the topic DNS.

DNS(Domain Name System) is the system where the human readable domain names are converted into IP addresses, that can be understood by the servers. Also it helps our query to find its respective servers so that we can access the site.

So we have the target website and as a common routine we can go with scanning(NMAP), to check whether is there any open ports.

<img width="746" height="335" alt="1_B5Ca6aJ6RFxuagzze7GrSA" src="https://github.com/user-attachments/assets/ef8e9620-a644-43a3-bf8a-245c6de2c5bb" />

From the simple port scanning we can come to the conclusion that there no direct http server at any other service that is running under the target IP.

The challenge description mentions “Oooh, turns out, this 10.48.188.156 machine is also a DNS server!”. So we can conclude that the target IP is a DNS server.

The next phrase goes like “If we could dig into it, I am sure we could find some interesting records” , so by learing aout the DNS, I found a tool that is named as DIG(Domain Information Groper).

So then by the complete understanding of the description “ this only responds to a special type of request for a givemetheflag.com domain”, i thought that there would any hint under this site.

<img width="1100" height="592" alt="1_QFtr3YfqL5KgzLfzy7oALA" src="https://github.com/user-attachments/assets/9ba1f8d7-fb08-4686-8cf7-99c297628b53" />

But it was of no use.😶‍🌫️😶‍🌫️😶‍🌫️

So then by trying some methods finally i found the way to get the flag. So we need to send the givemetheflag.com request to a the targeted DNS server.

dig givemetheflag.com @10.48.188.156

And boom🎉🎉🎉🎉

<img width="825" height="540" alt="1_Hr5laHfGOYvunE5ubTKc0w" src="https://github.com/user-attachments/assets/810727ed-d608-48fa-8a2a-13741da3b839" />
