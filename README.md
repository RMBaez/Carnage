<h1>Carnage</h1>


<h2>Description</h2>
Eric Fischer from the Purchasing Department at Bartell Ltd has received an email from a known contact with a Word document attachment.  Upon opening the document, he accidentally clicked on "Enable Content."  The SOC Department immediately received an alert from the endpoint agent that Eric's workstation was making suspicious connections outbound. The pcap was retrieved from the network sensor and handed to you for analysis. 

Task: Investigate the packet capture and uncover the malicious activities. 

NOTE: DO NOT directly interact with any domains and IP addresses in this challenge. 

<h2>Questions</h2>

- <b>What was the date and time for the first HTTP connection to the malicious IP?
(answer format: yyyy-mm-dd hh:mm:ss)</b>
- <b>What is the name of the zip file that was downloaded?</b>
- <b>What was the domain hosting the malicious zip file?</b>
- <b>Without downloading the file, what is the name of the file in the zip file?</b>
- <b>What is the name of the webserver of the malicious IP from which the zip file was downloaded?</b>
- <b>What is the version of the webserver from the previous question?</b>
- <b>Malicious files were downloaded to the victim host from multiple domains. What were the three domains involved with this activity?</b>
- <b>Which certificate authority issued the SSL certificate to the first domain from the previous question?</b>
- <b>What are the two IP addresses of the Cobalt Strike servers? Use VirusTotal (the Community tab) to confirm if IPs are identified as Cobalt Strike C2 servers. (answer format: - enter the IP addresses in sequential order)</b>
- <b>What is the Host header for the first Cobalt Strike IP address from the previous question?</b>
- <b>What is the domain name for the first IP address of the Cobalt Strike server? You may use VirusTotal to confirm if it's the Cobalt Strike server (check the Community tab).</b>
- <b>What is the domain name of the second Cobalt Strike server IP?  You may use VirusTotal to confirm if it's the Cobalt Strike server (check the Community tab).</b>
- <b>What is the domain name of the post-infection traffic?</b>
- <b>What are the first eleven characters that the victim host sends out to the malicious domain involved in the post-infection traffic?</b>
- <b>What was the length for the first packet sent out to the C2 server?</b>
- <b>What was the Server header for the malicious domain from the previous question?</b>
- <b>The malware used an API to check for the IP address of the victim’s machine. What was the date and time when the DNS query for the IP check domain occurred? (answer format: yyyy-mm-dd hh:mm:ss UTC)</b>
- <b>What was the domain in the DNS query from the previous question?</b>
- <b>Looks like there was some malicious spam (malspam) activity going on. What was the first MAIL FROM address observed in the traffic?</b>
- <b>How many packets were observed for the SMTP traffic?</b>


<h2>Languages and Utilities Used</h2>

- <b>Wireshark</b> 


<h2>Environments Used </h2>

- <b>TryHackMe VM</b> 

<h2>Program walk-through</h2>

<b>Answer the question below <br/>

What was the date and time for the first HTTP connection to the malicious IP?
(answer format: yyyy-mm-dd hh:mm:ss)?

<p align="center">
To get the complete total number of events, we must first set the time filter to "All Time"(enclosed in pink on the top right). Then I input "index=main" on the search bar. The answer is enclosed in the red box. <br/>
<img width="1440" alt="Screenshot 2025-04-15 at 12 19 26 PM" src="https://github.com/user-attachments/assets/ef61c4eb-b481-4dec-baa5-3f5069cc5b2d" />


<br />
<br />
Answer is ------ <br/>





<h2>Program walk-through</h2>

<b>Answer the question below <br/>
What is the name of the zip file that was downloaded?

<p align="center">
The question states the adversaty CREATING a backdoor user. I googled the event id associated with user creation and recieved event id 4720. I then added EventID=4720 into the search bar. I scrolled down and found the newly created user. At a quick glance it might read Alberto but the "l" is actually a "1" thus giving the answer.    <br/>
<img width="1440" alt="image" src="https://github.com/user-attachments/assets/e77b5546-f0b4-47fc-88db-8ea4b0051113" />
<img width="1440" alt="image" src="https://github.com/user-attachments/assets/e13a9add-d45e-4f67-9e21-d4a601e6cb01" />
<img width="1440" alt="Screenshot 2025-04-15 at 12 35 46 PM" src="https://github.com/user-attachments/assets/74aa703f-b5d0-4eca-b7eb-2b1cd55fc5b0" />




<br />
<br />
Answer is ----- <br/>




<h2>Program walk-through</h2>

<b>Answer the question below <br/>
What was the domain hosting the malicious zip file?


<p align="center">
We now know which device the user A1berto was created on. <img width="1440" alt="Screenshot 2025-04-15 at 12 42 58 PM" src="https://github.com/user-attachments/assets/410b3f31-0e99-452d-a84d-25bf5fcd724b" /> <br/>

  
We add Micheal.Beaven in the seach bar
<img width="1440" alt="image" src="https://github.com/user-attachments/assets/7ad5b04f-82e5-441f-88ac-cde3c3f14371" />

  
To find the answer I did a few things. Frist, I google for the event id that was associated with registry modification. The event id I received and inputted resulted in zero events. I removed the attempted event id search and instead, I then added the user "A1berto" into the search bar since the user "A1berto" is still the topic. It helped to reduced the number of events low enough where I wouldn't mind scrolling and reading through the events to find the answer. However, I want to be a bit more precise. I looked through the fields and found "extracted_EventType" which caught my eye. I clicked it and saw CreateKey so I added that into my search resulting in 1 event.
<img width="1440" alt="Screenshot 2025-04-15 at 1 11 52 PM" src="https://github.com/user-attachments/assets/7ee146cd-e597-4777-9b80-ad9c98b649d2" />
<img width="1440" alt="image" src="https://github.com/user-attachments/assets/5025cc9a-d8b0-4bde-98bd-2e1cbc0edc0d" />


I scrolled down and under the field "Target_Object" the answer appears.
<img width="1440" alt="Screenshot 2025-04-15 at 1 16 33 PM" src="https://github.com/user-attachments/assets/21d3fae0-3243-4c74-99de-b65a400e6c24" />




<br />
<br />
Answer is ------ <br/>






<h2>Program walk-through</h2>

<b>Answer the question below <br/>
Without downloading the file, what is the name of the file in the zip file?

<p align="center">
The answer was dicussed in an earlier question. User A1berto is impersonating Alberto


<br />
<br />
Answer is ----- <br/>



<h2>Program walk-through</h2>

<b>Answer the question below <br/>

What is the name of the webserver of the malicious IP from which the zip file was downloaded?

<p align="center">
I knew to look for an executable file(.exe). Since the question asked what command was used, I looked the a field containing the word command and "CommandLine" appeared. I did a quick look at it and saw one that looked suspicious. I decided to seach the field "CommandLine" as a wildcard just to not overlook anything. Also, I once again added user "A1berto" to focus the search. <br/>
<img width="1440" alt="image" src="https://github.com/user-attachments/assets/c295758a-0cf0-42ab-be0c-7f12cb61cc74" />

  
With 7 results I looked through them all. Looking at each CommandLine field within the events, the one that had looked suspicious to me was the answer to the question.
<img width="1440" alt="Screenshot 2025-04-15 at 1 37 12 PM" src="https://github.com/user-attachments/assets/8d058594-06b9-4abf-b23c-5d9dbc1f936f" />

After looking at how others solved this question, there is a more efficient way. There is an event id associated with program execution (Event ID 4688)
<img width="1440" alt="image" src="https://github.com/user-attachments/assets/1b2a15b3-7489-4844-831e-0e2871c29a48" />
The full search should be " index=main EventID=4688 A1berto ". Look at the CommandLine field and you'll find the same answer. Through this search I learned that WMIC is a software utility that allows users to perform Windows Management Instrumentation operations with a command prompt. That ransomware authors have been seen to use wmic.exe to gain access to remote systems and then perform processes on it to prepare for or execute the ransomware attack.
<img width="1440" alt="Screenshot 2025-04-15 at 1 50 01 PM" src="https://github.com/user-attachments/assets/ad356081-fbc7-434e-ad31-fe34cf339e34" />




<br />
<br />
Answer is --------- <br/>





<h2>Program walk-through</h2>

<b>Answer the question below <br/>

What is the version of the webserver from the previous question?


<p align="center">
To get the complete total number of events, we must first set the time filter to "All Time"(enclosed in pink on the top right). Then I input "index=main" on the search bar. The answer is enclosed in the red box. <br/>
<img width="1440" alt="Screenshot 2025-04-15 at 12 19 26 PM" src="https://github.com/user-attachments/assets/ef61c4eb-b481-4dec-baa5-3f5069cc5b2d" />


<br />
<br />
Answer is ------ <br/>





<h2>Program walk-through</h2>

<b>Answer the question below <br/>
Malicious files were downloaded to the victim host from multiple domains. What were the three domains involved with this activity?

<p align="center">
The question states the adversaty CREATING a backdoor user. I googled the event id associated with user creation and recieved event id 4720. I then added EventID=4720 into the search bar. I scrolled down and found the newly created user. At a quick glance it might read Alberto but the "l" is actually a "1" thus giving the answer.    <br/>
<img width="1440" alt="image" src="https://github.com/user-attachments/assets/e77b5546-f0b4-47fc-88db-8ea4b0051113" />
<img width="1440" alt="image" src="https://github.com/user-attachments/assets/e13a9add-d45e-4f67-9e21-d4a601e6cb01" />
<img width="1440" alt="Screenshot 2025-04-15 at 12 35 46 PM" src="https://github.com/user-attachments/assets/74aa703f-b5d0-4eca-b7eb-2b1cd55fc5b0" />




<br />
<br />
Answer is ----- <br/>




<h2>Program walk-through</h2>

<b>Answer the question below <br/>
Which certificate authority issued the SSL certificate to the first domain from the previous question?


<p align="center">
We now know which device the user A1berto was created on. <img width="1440" alt="Screenshot 2025-04-15 at 12 42 58 PM" src="https://github.com/user-attachments/assets/410b3f31-0e99-452d-a84d-25bf5fcd724b" /> <br/>

  
We add Micheal.Beaven in the seach bar
<img width="1440" alt="image" src="https://github.com/user-attachments/assets/7ad5b04f-82e5-441f-88ac-cde3c3f14371" />

  
To find the answer I did a few things. Frist, I google for the event id that was associated with registry modification. The event id I received and inputted resulted in zero events. I removed the attempted event id search and instead, I then added the user "A1berto" into the search bar since the user "A1berto" is still the topic. It helped to reduced the number of events low enough where I wouldn't mind scrolling and reading through the events to find the answer. However, I want to be a bit more precise. I looked through the fields and found "extracted_EventType" which caught my eye. I clicked it and saw CreateKey so I added that into my search resulting in 1 event.
<img width="1440" alt="Screenshot 2025-04-15 at 1 11 52 PM" src="https://github.com/user-attachments/assets/7ee146cd-e597-4777-9b80-ad9c98b649d2" />
<img width="1440" alt="image" src="https://github.com/user-attachments/assets/5025cc9a-d8b0-4bde-98bd-2e1cbc0edc0d" />


I scrolled down and under the field "Target_Object" the answer appears.
<img width="1440" alt="Screenshot 2025-04-15 at 1 16 33 PM" src="https://github.com/user-attachments/assets/21d3fae0-3243-4c74-99de-b65a400e6c24" />




<br />
<br />
Answer is ------ <br/>






<h2>Program walk-through</h2>

<b>Answer the question below <br/>
What are the two IP addresses of the Cobalt Strike servers? Use VirusTotal (the Community tab) to confirm if IPs are identified as Cobalt Strike C2 servers. (answer format: enter the IP addresses in sequential order)

<p align="center">
The answer was dicussed in an earlier question. User A1berto is impersonating Alberto


<br />
<br />
Answer is ----- <br/>



<h2>Program walk-through</h2>

<b>Answer the question below <br/>

What is the Host header for the first Cobalt Strike IP address from the previous question?

<p align="center">
I knew to look for an executable file(.exe). Since the question asked what command was used, I looked the a field containing the word command and "CommandLine" appeared. I did a quick look at it and saw one that looked suspicious. I decided to seach the field "CommandLine" as a wildcard just to not overlook anything. Also, I once again added user "A1berto" to focus the search. <br/>
<img width="1440" alt="image" src="https://github.com/user-attachments/assets/c295758a-0cf0-42ab-be0c-7f12cb61cc74" />

  
With 7 results I looked through them all. Looking at each CommandLine field within the events, the one that had looked suspicious to me was the answer to the question.
<img width="1440" alt="Screenshot 2025-04-15 at 1 37 12 PM" src="https://github.com/user-attachments/assets/8d058594-06b9-4abf-b23c-5d9dbc1f936f" />

After looking at how others solved this question, there is a more efficient way. There is an event id associated with program execution (Event ID 4688)
<img width="1440" alt="image" src="https://github.com/user-attachments/assets/1b2a15b3-7489-4844-831e-0e2871c29a48" />
The full search should be " index=main EventID=4688 A1berto ". Look at the CommandLine field and you'll find the same answer. Through this search I learned that WMIC is a software utility that allows users to perform Windows Management Instrumentation operations with a command prompt. That ransomware authors have been seen to use wmic.exe to gain access to remote systems and then perform processes on it to prepare for or execute the ransomware attack.
<img width="1440" alt="Screenshot 2025-04-15 at 1 50 01 PM" src="https://github.com/user-attachments/assets/ad356081-fbc7-434e-ad31-fe34cf339e34" />






<br />
<br />
Answer is --------- <br/>





