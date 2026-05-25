<img width="1100" height="466" alt="1_rhrRgFy47blYHlqV2Ba2EQ" src="https://github.com/user-attachments/assets/c75132ca-38e6-462d-b91d-f74cbb783939" />
So this was one of by favorite room that made me to try a lot and took a much time. But it can be solved in a much soon if i noticed the basic of website that is Headers.

I went through the webpage and tried to find whether is there any loop holes. I checked in the search bar whether there’s any directory reversal and stuffs like that. But nothing worked.It was a static webpage and no connection from the backend. So can’t retrieve any details from the backend.

<img width="1100" height="539" alt="1_f4XTyNNJpuNt04g3Iy4dfw" src="https://github.com/user-attachments/assets/43c2ba96-865e-46ea-8ddb-fae81c8226fb" />

Then after lots of attempts and going through the webpage nothing can be found as vulnerable. So tried of using the hint. And boom😶‍🌫️, by checking the headers there was an vulnerablity.

<img width="727" height="527" alt="1_yjcbJXuU91tkegGQriZYUg" src="https://github.com/user-attachments/assets/5ff016ac-6ad9-4183-9daa-25036fcdb9cb" />

The PHP/8.1.0-dev is an vulnerablity.

PHP 8.1.0-dev — ‘User-Agentt’ Remote Code Execution

By surfing in the google it was found vulnerable and can be exploited by adding the ‘t’ in the “useragent” section of the header where the RCE can be executed.

User-Agentt: zerodiumsystem(‘cat /flag.txt’);

The explanation can be viewed in the google and adding the ‘;’ in last is important as the above code will act as an code in the php.

<img width="1100" height="575" alt="1_wuTD47Wq_jUeijRnh1WkIA" src="https://github.com/user-attachments/assets/c37fbab0-b2a9-444b-a2cd-eea46c75372e" />

So one of the most important learning is don’t avoid any information, the vulnerable can be found at any place.




