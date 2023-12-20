<font size = '4'>
<p align = 'center'>
<b>
Advent of Cyber - Day 7 Writeup 
</b>
</p>
</font>

<br>
<font size = '3'>

<b>Introduction: </b>
This writeup provides a solution to Day 7 of the Advent of Cyber 2023 challenge titled "Proxy Log Analysis." In this task, Tracy McGreedy, seeking revenge for a demotion, installs the CrypTOYminer malware on company workstations. Forensic McBlue assembles a team to analyze proxy logs and identify suspicious network activity.

<b>Author:</b> Misha Jain

<b>Date:</b> December 7, 2023

<b>Tools Used:</b><br>
- Linux command-line tools: cut, sort, uniq, grep, base64
- Web browser for accessing the challenge environment

<b>Challenge Description:</b><br>
The challenge involves analyzing proxy logs to uncover potential security incidents related to the CrypTOYminer malware. The task requires interpreting log entries, understanding proxy servers, and using Linux command-line tools for log analysis.

<b>Exploitation:</b><br>
Go to the /artefacts directory using the cd command.<br><br>

<b>Questions and Answers:</b><br>
1. How many unique IP addresses are connected to the proxy server?
    - Command: cut -d ' ' -f2 access.log | sort -u | wc -l
    - Answer: 9

2. How many unique domains were accessed by all workstations?
    - Command: cut -d ' ' -f3 access.log | cut -d ':' -f1 | sort -u | wc -l
    - Answer: 111

3. What status code is generated by the HTTP requests to the least accessed domain?
     - Command: cut -d ' ' -f3,6 access.log | sort | uniq -c | sort -n | head -n 1
    - Answer: 503

4. Based on the high count of connection attempts, what is the name of the suspicious domain?
    - Command: cut -d ' ' -f3 access.log | sort | uniq -c | sort -nr
    - Answer: frostlings.bigbadstash.thm

5. What is the source IP of the workstation that accessed the malicious domain?
    - Commands: grep "frostlings.bigbadstash.thm" access.log | cut -d ' ' -f2 | sort | uniq
    - Answer: 10.10.185.225

6. How many requests were made on the malicious domain in total?
    - Commands: grep frostlings.bigbadstash.thm access.log | wc -l
    - Answer: 1581

7. Having retrieved the exfiltrated data, what is the hidden flag?
    - Commands: grep "frostlings.bigbadstash.thm" access.log | cut -d ' ' -f5 | cut -d '=' -f2 | base64 -d
    - Answer: THM{a_gift_for_you_awesome_analyst!}

<b>Lessons Learned:</b><br>
- Analyzing proxy logs for cybersecurity investigations.
- Utilizing Linux command-line tools for log parsing and analysis.
- Identifying and interpreting common log entry components.
- Recognizing malicious indicators in proxy logs, such as high connection counts and unusual domains.
- Decoding Base64-encoded strings in log entries for data extraction.
<br><br>

<b>Conclusion:</b><br>
Day 7 of Advent of Cyber 2023 provided a hands-on experience in cybersecurity investigation through proxy log analysis. Participants honed their skills in using Linux command-line tools to dissect log entries, identify suspicious patterns, and extract valuable information. The challenge emphasized the significance of thorough log analysis in uncovering potential security incidents, showcasing the practical application of skills in a real-world scenario.

</font>