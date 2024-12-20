# Linux Cronjobs & Challenge CTF

<h2>Description</h2>
In this Linux cronjobs task, I explored the /etc/cron, observed daily cronjobs, wrote my own cronjob as an attacker to execute notmalware.elf every 5 minutes, and completed a linux network, process, and cronjob ctf challenge.  

<h2>Languages and Utilities Used</h2>


- <b>Linux CLI</b>

<h2>Environments Used </h2>

- <b>Ubuntu</b> 

<br />
<br />
Printed the /etc/crontab to display the contents of the system-wide crontab file. Then listed and grepped to find all cron files/directories in the /etc directory. 

![1) ](https://github.com/user-attachments/assets/c21c04f7-273b-4086-bb62-fa542c4828a5)

<br />
<br />
Scrolling down will show more meta data about the event log. 

![2)](https://github.com/user-attachments/assets/d4995e56-7931-4fdb-90e1-cef4de34737c)

<br />
<br />  
I used "crontab -e" to use nano editor to write a persistent malware cronjob to run every 5 minutes. 

![3)](https://github.com/user-attachments/assets/66b70882-f8f7-42a4-8016-ec4e0a6f22e1)

<br />
<br />
I used "sudo ls -al /var/spool/cron/crontabs/" to list all files, including hidden ones, in the /var/spool/cron/crontabs/ directory with detailed information, executed with root privileges. Using "sudo crontab -u albert -l" to list the crontab entries for the user 'albert' with root privileges showing the cronjob created to run notmalware.elf.

![4)](https://github.com/user-attachments/assets/8fbe51ec-0593-4731-9f2f-398887c0bc0b)

<br />
<br />
Challenge prompt. 

![5) challenge prompt](https://github.com/user-attachments/assets/7b296493-b2c5-4a77-8196-73721d0bace3)

<br />
<br />
Using "sudo netstat -tnpl" shows a suspicious program named "kitty.meow" with a PID of 16018 listening over port 31337.

![6) q2 3 4](https://github.com/user-attachments/assets/ddb2c673-ebaf-430a-bbe8-aa59a3d9d292)

<br />
<br />
Using "sudo lsof -p 16018" helps list the full path of kitty.meow. USing "sudo ps -AFH | less | grep kitty.meow" shows the full command line used. 

![7) q 5 6](https://github.com/user-attachments/assets/fa208b44-20cd-4599-8c27-3afefdd67765)

<br />
<br />
Moving over to /proc/16018, I used "sudo ls -al exe" to show the executable process and generated a sha256 hash. 

![8) q7](https://github.com/user-attachments/assets/01e0389c-706b-407f-8e06-db8231b397a5)

<br />
<br />
Using "strings 16018" helps me find the strings within the kitty.meow malware and I identified a netcat utility within the malware string. 


![9) strings exe](https://github.com/user-attachments/assets/894e01db-e55c-43fa-81f5-ab037137c0e1)

<br />
<br />
catting out crontab in /etc shows the persistence mechanism /tmp/exfiltr8.sh.

![10)](https://github.com/user-attachments/assets/03cbc750-be4e-4eb4-bedc-ca2d7ee28df7)

<br />
<br />
Using crontab guru on the persistence cronjob shows it running at 5:45pm oon Oct 13th. 

![11)](https://github.com/user-attachments/assets/5015141e-4a39-43a9-b711-9eb327349b13)

<br />
<br />
