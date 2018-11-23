![alt text](https://github.com/Hechtov/Photos/blob/master/zBang/zBang%20tool.png "zBang risk assessment tool")  
  
**zBang is a special risk assessment tool that detects potential privileged account threats in the scanned network.**  
  
Organizations and red teamers can utilize zBang to identify potential attack vectors and improve the security posture of the network. The results can be analyzed with the graphic interface or by reviewing the raw output files.  
  
**The tool is built from five different scanning modules:**  
1.	**ACLight scan** - discovers the most privileged accounts that must be protected, including suspicious Shadow Admins.
2.	**Skeleton Key scan** - discovers Domain Controllers that might be infected by Skeleton Key malware.
3.	**SID History scan** - discovers hidden privileges in domain accounts with secondary SID (SID History attribute).
4.	**RiskySPNs scan** - discovers risky configuration of SPNs that might lead to credential theft of Domain Admins
5.	**Mystique scan** - discovers risky Kerberos delegation configuration in the network.  
  
# Execution Requirements
1.	Run it with any domain user. The scans do not require any extra privileges; the tool performs read-only LDAP queries to the DC.
2.	Run the tool from a domain joined machine (a Windows machine).
3.	PowerShell version 3 or above and .NET 4.5 (it comes by default in Windows 8/2012 and above).
  
# Quick Start Guide
1.	Download and run the release version from this GitHub repository [link] or compile it with your favorite compiler.
2.	In the opening screen, choose what scans you wish to execute.  
In the following example, all five scans are chosen:  
![alt text](https://github.com/Hechtov/Photos/blob/master/zBang/opening%20menu.png "Opening menu")  
3.	To view demo results, click “Reload.”  
zBang tool comes with built-in initiating demo data; you can view the results of the different scans and play with the graphic interface.
4.	To initiate new scans in your network, click “Launch.” A new window will pop up and will display the status of the different scans.
![alt text](https://github.com/Hechtov/Photos/blob/master/zBang/aclight.png "Scan in progress") 
5.	When the scans are completed, there will be a message saying the results were exported to an external zip file.
![alt text](https://github.com/Hechtov/Photos/blob/master/zBang/zbang%20finished.png "Scan is finished")  
6.	The results zip file will be in the same folder of zBang and will have a unique name with the time and the date of the scans. You can also import previous results into the zBang GUI without the need of rerunning the scans.  
To import previous results, click “Import” in the zBang’s opening screen.  
  
# Go Over zBang Results:
a.	ACLight scan:
![alt text](https://github.com/Hechtov/Photos/blob/master/zBang/aclight%20result.png "ACLight results")  
i.	Choose the domain you have scanned.
ii.	You will see a list of the most privileged accounts that were discovered.
iii.	On the left side - view “standard” privileged accounts that get their privileges due to their group membership.
iv.	On the right side - view “Shadow Admins.” Those accounts get their privileges through direct ACL permissions assignment. Those accounts might be stealthier than standard “domain admin” users, and therefore, they might not be as secure as they should be. Attackers often target and try to compromise such accounts. 
v.	On each account, you can double click and review its permissions graph. It may help you understand why this account was classified as privileged.
![alt text](https://github.com/Hechtov/Photos/blob/master/zBang/aclight%20tree.png "ACLight permissions tree")
vi.	The different abusable ACL permissions are described in a small help page. Click the “question mark” in the upper right corner to view:  
![alt text](https://github.com/Hechtov/Photos/blob/master/zBang/risky%20ACLs.png "The abusable ACLs")  
vii.	More details on the threat of Shadow Admins are available in the blog post -
“Shadow Admins – The Stealthy Accounts That You Should Fear The Most”:
https://www.cyberark.com/threat-research-blog/shadow-admins-stealthy-accounts-fear/
viii.	For manual examination of the scan results,  unzip the saved zBang results file and check the results folder:
"[Path of the zBang’s unzipped results file]\ACLight-master\Results”, contains a summary report - “Privileged Accounts - Layers Analysis.txt”.
ix.	On each of the discovered privileged accounts: 
1.	Identify the privileged account.
2.	Reduce unnecessary permissions from the account.
3.	Secure the account. After validating these three steps, you can mark the account with a “V” in the small selection box, turning it green on the interface.
x.	The goal is to make all the accounts marked as “secured” with the green color.
  
b.	Skeleton Key scan
i.	In the scan page (click the relevant bookmark in the above section), there will be a list of all the scanned DCs. 
ii.	Make sure all of them are clean and marked with green.
iii.	If the scan finds a potential infected DC, it is crucial to initiate an investigation process.
![alt text](https://github.com/Hechtov/Photos/blob/master/zBang/skeleton%20key.png "The abusable ACLs")  
iv.	More details on Skeleton Key malware are available in the blog post
“Active Directory Domain Controller Skeleton Key Malware & Mimikatz” by @PyroTek3: https://adsecurity.org/?p=1255
  
  




