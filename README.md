<h1>Carnage</h1>


<h2>Description</h2>
Eric Fischer from the Purchasing Department at Bartell Ltd has received an email from a known contact with a Word document attachment.  Upon opening the document, he accidentally clicked on "Enable Content."  The SOC Department immediately received an alert from the endpoint agent that Eric's workstation was making suspicious connections outbound. The pcap was retrieved from the network sensor and handed to you for analysis. 

Task: Investigate the packet capture and uncover the malicious activities. 

NOTE: DO NOT directly interact with any domains and IP addresses in this challenge. Answers will be in defang format.

<h2>Questions</h2>

- <b>1. What was the date and time for the first HTTP connection to the malicious IP?
(answer format: yyyy-mm-dd hh:mm:ss)</b>
- <b>2. What is the name of the zip file that was downloaded?</b>
- <b>3. What was the domain hosting the malicious zip file?</b>
- <b>4. Without downloading the file, what is the name of the file in the zip file?</b>
- <b>5. What is the name of the webserver of the malicious IP from which the zip file was downloaded?</b>
- <b>6. What is the version of the webserver from the previous question?</b>
- <b>7. Malicious files were downloaded to the victim host from multiple domains. What were the three domains involved with this activity?</b>
- <b>8. Which certificate authority issued the SSL certificate to the first domain from the previous question?</b>
- <b>9. What are the two IP addresses of the Cobalt Strike servers? Use VirusTotal (the Community tab) to confirm if IPs are identified as Cobalt Strike C2 servers. (answer format: - enter the IP addresses in sequential order)</b>
- <b>10. What is the Host header for the first Cobalt Strike IP address from the previous question?</b>
- <b>11. What is the domain name for the first IP address of the Cobalt Strike server? You may use VirusTotal to confirm if it's the Cobalt Strike server (check the Community tab).</b>
- <b>12. What is the domain name of the second Cobalt Strike server IP?  You may use VirusTotal to confirm if it's the Cobalt Strike server (check the Community tab).</b>
- <b>13. What is the domain name of the post-infection traffic?</b>
- <b>14. What are the first eleven characters that the victim host sends out to the malicious domain involved in the post-infection traffic?</b>
- <b>15. What was the length for the first packet sent out to the C2 server?</b>
- <b>16. What was the Server header for the malicious domain from the previous question?</b>
- <b>17. The malware used an API to check for the IP address of the victim’s machine. What was the date and time when the DNS query for the IP check domain occurred? (answer format: yyyy-mm-dd hh:mm:ss UTC)</b>
- <b>18. What was the domain in the DNS query from the previous question?</b>
- <b>19. Looks like there was some malicious spam (malspam) activity going on. What was the first MAIL FROM address observed in the traffic?</b>
- <b>20. How many packets were observed for the SMTP traffic?</b>


<h2>Languages and Utilities Used</h2>

- <b>Wireshark</b> 


<h2>Environments Used </h2>

- <b>TryHackMe VM</b> 

<h2>Program walk-through</h2>

<b>Answer the question below <br/>

1. What was the date and time for the first HTTP connection to the malicious IP?
(answer format: yyyy-mm-dd hh:mm:ss)?

<p align="center">
I simply filtered the packets to show HTTP, and checked the first frame’s details: <br/>
  
<img width="1440" alt="Screenshot 2025-06-01 at 11 51 31 AM" src="https://github.com/user-attachments/assets/90621771-0707-469f-90ec-03c23290d44c" />


<br />
<br />
Answer is 2021-09-24 16:44:38 <br/>





<h2>Program walk-through</h2>

<b>Answer the question below <br/>
2. What is the name of the zip file that was downloaded?

<p align="center">
the first HTTP GET (Frame 1735) contains the zip file I needed <br/>
<img width="1440" alt="Screenshot 2025-06-01 at 12 00 41 PM" src="https://github.com/user-attachments/assets/bc253aa9-e68d-4a25-9977-266ec76426f4" />




<br />
<br />
Answer is documents[.]zip <br/>




<h2>Program walk-through</h2>

<b>Answer the question below <br/>
3. What was the domain hosting the malicious zip file?


<p align="center">
I looked into the frame details. Upon looking at the Hypertext Transfer Protocol section. Where it says Host, there is the answer. <br/>

  <img width="1440" alt="Screenshot 2025-06-01 at 12 04 09 PM" src="https://github.com/user-attachments/assets/dbbea3e5-c0e4-4ada-86e2-d915b3252de1" />



<br />
<br />
Answer is attirenepal[.]com <br/>




<h2>Program walk-through</h2>

<b>Answer the question below <br/>
4. Without downloading the file, what is the name of the file in the zip file?

<p align="center">
In packet 1735 under the Hypertext Transfer Protocol section, it said that the response packet was 2173, so I went there. Once there, I decided to open up a HTTP Stream for easier reading. Not long into reading the hex, I spotted something that looked like a possible file name recognzing the "xls" as a file type and the filename looked suspicious.


<br />
<br />
Answer is chart-1530076591[.]xls <br/>



<h2>Program walk-through</h2>

<b>Answer the question below <br/>

5. What is the name of the webserver of the malicious IP from which the zip file was downloaded?

<p align="center">
I kept the HTTP Stream for packet 2173 open for this question. There is a line that says 'server' and there is the answer <br/>
  
<img width="1440" alt="Screenshot 2025-06-01 at 12 42 50 PM" src="https://github.com/user-attachments/assets/7907b939-1481-4db8-939d-7db1b623ce33" />


<br />
<br />
Answer LiteSpeed <br/>





<h2>Program walk-through</h2>

<b>Answer the question below <br/>

6. What is the version of the webserver from the previous question?


<p align="center">
I kept the HTTP Stream for packet 2173 open for this question. There is a line that says 'x-powered-by' and there is the answer <br/>
<img width="1440" alt="Screenshot 2025-06-01 at 3 18 53 PM" src="https://github.com/user-attachments/assets/252e6b48-9362-4a26-a065-ca564db0e85f" />



<br />
<br />
Answer is PHP/7.2.34 <br/>





<h2>Program walk-through</h2>

<b>Answer the question below <br/>
7. Malicious files were downloaded to the victim host from multiple domains. What were the three domains involved with this activity?

<p align="center">
There was a hint to this question and it said 'Check HTTPS traffic. Narrow down the timeframe from 16:45:11 to 16:45:30.' To be honest... without this hint, I wouldn't have known how to even begin to find the answer to this question. HTTPS uses encryption for secured communication over computer networks and TLS is used to encrypt the communication protocol. I used the filter tls.handshake.type==1 and received 181 results. I needed to add more filters to minimize the results. I didn't know how to manually write the filter for focusing on the given timeframe so in the packet details in the Frame section, I right clicked on the arrival time and added it into the display filter. I did it twice and modified the time according to the hint given. The completed filter used was : ((tls.handshake.type==1 ) && (frame.time >= "Sep 24, 2021 16:45:11") ) && (frame.time <= "Sep 24, 2021 16:45:30"). I then went to Preferences, went to name resolution and checked resolved network (IP) addresses. I found the answers to the question.     <br/>
<img width="1440" alt="Screenshot 2025-06-01 at 4 20 34 PM" src="https://github.com/user-attachments/assets/8e7ee4c1-7a92-4f3d-bd92-bc7c8c7b4295" />
<img width="1440" alt="Screenshot 2025-06-01 at 4 23 16 PM" src="https://github.com/user-attachments/assets/8c4054bd-d63f-415d-8af5-0825c08b35ac" />
<img width="1440" alt="Screenshot 2025-06-01 at 4 39 09 PM" src="https://github.com/user-attachments/assets/b30d78d1-35d0-4c55-a4a1-fb9a4c5f0e25" />
<img width="1440" alt="Screenshot 2025-06-01 at 4 44 28 PM" src="https://github.com/user-attachments/assets/aa81bd53-35fd-48c2-a083-bc3da09e8eaf" />
<img width="1440" alt="Screenshot 2025-06-01 at 4 46 37 PM" src="https://github.com/user-attachments/assets/015f9bf0-558b-4d55-8e70-95016fcc754e" />


<br />
<br />
Answer is finejewels[.]com[.]au, thietbiagt[.]com, new[.]americold[.]com <br/>


<h2>Program walk-through</h2>

<b>Answer the question below <br/>
8. Which certificate authority issued the SSL certificate to the first domain from the previous question?


<p align="center">
I TCP streamed the first packet since that is where the first domain was located. I typed in Certificate Authority on the find section to help enhance my search. I found it right away. <br/>
<img width="1440" alt="Screenshot 2025-06-01 at 5 15 13 PM" src="https://github.com/user-attachments/assets/a16902a5-5760-417c-8e4c-23876e765083" />


<br />
<br />
Answer is GoDaddy <br/>






<h2>Program walk-through</h2>

<b>Answer the question below <br/>
9. What are the two IP addresses of the Cobalt Strike servers? Use VirusTotal (the Community tab) to confirm if IPs are identified as Cobalt Strike C2 servers. (answer format: enter the IP addresses in sequential order)

<p align="center">
The hint given for this question is "Check the Conversations menu option" and I did exactly just that. I had VirusTotal on another tab. What I did was reordered the 'Address B' table to organize all IPs. I copied and pasted every IP into VirusTotal until I found the 2 IPs that belong to the Cobalt Strike servers. 
<img width="1440" alt="Screenshot 2025-06-01 at 5 52 58 PM" src="https://github.com/user-attachments/assets/680ab83c-0b10-4d6a-ac6e-d4618bb03444" />


<br />
<br />
Answer is 185[.]106[.]96[.]158, 185[.]125[.]204[.]174 <br/>



<h2>Program walk-through</h2>

<b>Answer the question below <br/>

10. What is the Host header for the first Cobalt Strike IP address from the previous question?

<p align="center">
I entered into the display filter: ip.dst==185[.]106[.]96[.]158. I went to the packet with the first GET request. Went into the HyperText Transfer Protocol section and there found the answer. <br/>
<img width="1440" alt="Screenshot 2025-06-01 at 6 05 37 PM" src="https://github.com/user-attachments/assets/92ecd630-c31f-4f3d-a0bc-7605884b6dfa" />


<br />
<br />
Answer is ocsp[.]verisign[.]com <br/>





<h2>Program walk-through</h2>

<b>Answer the question below <br/>

11. What is the domain name for the first IP address of the Cobalt Strike server? You may use VirusTotal to confirm if it's the Cobalt Strike server (check the Community tab).

<p align="center">
I filtered the first IP address into the display filter. I then went to Preferences, went to name resolution and checked resolved network (IP) addresses. I found the answers to the question. <br/>
<img width="1440" alt="Screenshot 2025-06-01 at 6 32 47 PM" src="https://github.com/user-attachments/assets/6fb9cd71-0280-451b-974b-6e5eea886d69" />



<br />
<br />
Answer is survmeter[.]live <br/>





<h2>Program walk-through</h2>

<b>Answer the question below <br/>
12. What is the domain name of the second Cobalt Strike server IP?  You may use VirusTotal to confirm if it's the Cobalt Strike server (check the Community tab).

<p align="center">
I couldn't find the answer using the same method as the previous question so I copy and pasted the second IP address into VirusTotal and got the answer.. <br/>

<br />
<br />
Answer is securitybusinpuff[.]com <br/>




<h2>Program walk-through</h2>

<b>Answer the question below <br/>
13. What is the domain name of the post-infection traffic?


<p align="center">
In the display filter I put: http.request.method==POST. I had left the name resolution preference on. <br/>
<img width="1440" alt="Screenshot 2025-06-01 at 6 55 39 PM" src="https://github.com/user-attachments/assets/9b2f872a-fb82-40a4-b361-b58d146beced" />

  

<br />
<br />
Answer is maldivehost[.]net <br/>





<h2>Program walk-through</h2>

<b>Answer the question below <br/>
14. What are the first eleven characters that the victim host sends out to the malicious domain involved in the post-infection traffic? 

<p align="center">
In the packet list, in the section where it says 'Info', there is the answer.
<img width="1440" alt="Screenshot 2025-06-01 at 7 07 22 PM" src="https://github.com/user-attachments/assets/800d25aa-f93e-4d20-9650-19afca0b442a" />



<br />
<br />
Answer is zLIisQRWZI <br/>



<h2>Program walk-through</h2>

<b>Answer the question below <br/>

15. What was the length for the first packet sent out to the C2 server?

<p align="center">
In the packet list in the section where it says 'length' is the answer. <br/>
<img width="1440" alt="Screenshot 2025-06-01 at 7 12 18 PM" src="https://github.com/user-attachments/assets/2733e5e0-3763-4dc4-8130-2665b01e6e1d" />


<br />
<br />
Answer is 281 <br/>




<h2>Program walk-through</h2>

<b>Answer the question below <br/>
16. What was the Server header for the malicious domain from the previous question?


<p align="center">
On the packet, I opened the HTTP Stream. Looked for server and found it.  <br/>
<img width="1440" alt="Screenshot 2025-06-01 at 7 24 37 PM" src="https://github.com/user-attachments/assets/35cd3ddb-7746-4808-9e39-5a136dd5a79b" />



<br />
<br />
Answer is Apache/2.4.49 (cPanel) OpenSSL/1.1.1l mod_bwlimited/1.4 <br/>





<h2>Program walk-through</h2>

<b>Answer the question below <br/>
17. The malware used an API to check for the IP address of the victim’s machine. What was the date and time when the DNS query for the IP check domain occurred? (answer format: yyyy-mm-dd hh:mm:ss UTC)

<p align="center">
In the display filter, I put in: dns contains "api". That left me with 10 results.    <br/>
  
<img width="1440" alt="Screenshot 2025-06-01 at 7 59 40 PM" src="https://github.com/user-attachments/assets/046f8ccc-e7a2-42dd-b097-336a7657de3c" />



<br />
<br />
Answer is 2021-09-24 17:00:04 <br/>






<h2>Program walk-through</h2>

<b>Answer the question below <br/>
18. What was the domain in the DNS query from the previous question?


<p align="center">
Take a look in the info tab from the previous question and the answer is there.  <br/>
  
<img width="1440" alt="Screenshot 2025-06-01 at 8 01 39 PM" src="https://github.com/user-attachments/assets/547839c0-94f7-40c0-b8ce-01524955acde" />



<br />
<br />
Answer is api[.]ipify[.]org <br/>



<h2>Program walk-through</h2>

<b>Answer the question below <br/>
19. Looks like there was some malicious spam (malspam) activity going on. What was the first MAIL FROM address observed in the traffic?

<p align="center">
I entered in the display filter: frame contains "MAIL FROM" and received 11 results. The question asked for the first 'MAIL FROM' address. Went to the packet bytes section and found the answer.


<br />
<br />
Answer is farshin@mailfa[.]com <br/>



<h2>Program walk-through</h2>

<b>Answer the question below <br/>

20. How many packets were observed for the SMTP traffic?

<p align="center">
I filtered 'smtp' into the display filter. Looked where it says displayed on the bottom right of the screen <br/>
<img width="1440" alt="Screenshot 2025-06-01 at 8 16 12 PM" src="https://github.com/user-attachments/assets/b888bb6a-4346-4259-bca3-66352d3a975e" />





<br />
<br />
Answer is 1439 <br/>






