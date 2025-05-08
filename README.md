## Threat Hunt Scenario 1
#### Investigating VMs that have mistakenly been exposed to the public internet.

### - Preparation
> [!NOTE]
> Set up the hunt by defining what you're looking for:<BR><BR>
During routine maintenance, the security team is tasked with investigating any VMs in the shared services cluster (handling DNS, Domain Services, DHCP, etc.) that have mistakenly been exposed to the public internet. The goal is to identify any misconfigured VMs and check for potential brute-force login attempts/successes from external sources.
Activity: Develop a hypothesis based on threat intelligence and security gaps (e.g., “Could there be lateral movement in the network?”).
During the time the devices were unknowingly exposed to the internet, it’s possible that someone could have actually brute-force logged into some of them since some of the older devices do not have account lockout configured for excessive failed login attempts.
### - Data Collection
> [!TIP]
> Gather relevant data from logs, network traffic, and endpoints.<BR><BR>
Consider inspecting the logs to see which devices have been exposed to the internet and have received excessive failed login attempts. Take note of the source IP addresses and number of failures, etc.
Activity: Ensure data is available from all key sources for analysis.
Ensure the relevant tables contain recent logs:<br><br>
DeviceInfo<br>
DeviceLogonEvents
### - Data Analysis
> [!TIP]
> Analyze data to test your hypothesis.
Activity: Look for anomalies, patterns, or indicators of compromise (IOCs) using various tools and techniques.
Is there any evidence of brute force success (many failed logins followed by a success?) on your VM or ANY VMs in the environment?
If so, what else happened on that machine around the same time? Were any bad actors able to log in?
### - Investigation
> [!WARNING]
> Investigate any suspicious findings.
Activity: Dig deeper into detected threats, determine their scope, and escalate if necessary. See if anything you find matches TTPs within the MITRE ATT&CK Framework.
You can use ChatGPT to figure this out by pasting/uploading the logs: Scenario 1: TTPs
### - Response
> [!WARNING]
> Mitigate any confirmed threats.
Activity: Work with security teams to contain, remove, and recover from the threat.
Can anything be done?
### - Documentation
> [!NOTE]
> Record your findings and learn from them.
Activity: Document what you found and use it to improve future hunts and defenses.
Document what you did
### - Improvement
> [!IMPORTANT]
> Improve your security posture or refine your methods for the next hunt. 
Activity: Adjust strategies and tools based on what worked or didn’t.
Anything we could have done to prevent the thing we hunted for? Any way we could have improved our hunting process?

## Notes / Findings:

### Timeline Summary and Findings:

VM-MDE-Test-CJ has been internet facing for several days

DeviceInfo<BR>
| where DeviceName == "vm-mde-test-cj"<BR>
| where IsInternetFacing == true<BR>
| order by Timestamp desc<BR>

Last interfacing time: 2025-05-02T01:00:39.654423Z___

Using KQL to check for any bad actors that may have been attempting to log into the target network:<BR><BR>
![KQL Code](https://github.com/user-attachments/assets/119f2014-ba96-4bc0-b010-4cae58452298)<BR><BR>
The following results show that none of the attempted logins were suspicious login attempts after exploring the TTP of the MITRE ATT&CK Framework. It is clear from my investigation that no T1110 Brute Force (MITRE ATT&CK Framework) logins were attempted.<BR><BR>
![KQL Code Findings](https://github.com/user-attachments/assets/f500c383-c0a5-4113-a0e0-02ff01d4279c)<BR><BR>

<p align="center">
  <img src="https://github.com/user-attachments/assets/4945b2bc-4737-4a33-a5bc-b1b23d7c2a86" alt="Description" width="400"/>
</p>
