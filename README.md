# HANDS ON DYNAMIC ANALYSIS 🧑‍💻

Download the following
- Any of malware sample https://zeltser.com/malware-sample-sources/
- [Regshot](https://sourceforge.net/projects/regshot/) for viewing before malware attack and after malware attack
- [procomon](https://learn.microsoft.com/en-us/sysinternals/downloads/procmon) for viewing Suspicious activities of malware
- [process hacker](https://processhacker.sourceforge.io/downloads.php) for viewing Suspicious activities of malware
- [Wireshark](https://www.wireshark.org/) for viewing which server the malware is connected and steals the data and send it to the malware author

 # Walkthrough analysis

 - Open the tabs of Process Hacker, Wireshark , Regshot 👍
 - Click to Wireshark "Ethernet"
 - Click to "1st shot"

<img src="https://github.com/Tripati3000/dynamic-ANALYSIS/assets/160244601/212f192d-fecb-4eb5-9446-4d95351f3a67" height="80%" width="80%" alt="SIEM System steps"/>

- it will take some time for 1st regshot
- After its completion open Procmon 👍

<img src="https://github.com/Tripati3000/dynamic-ANALYSIS/assets/160244601/d9446b20-2d35-4cd4-8641-cbbd2379aca8" height="80%" width="80%" alt="SIEM System steps"/>

- Now, Extract the malware sample you downloaded 
- Rename it to (filename`.exe`) exe means it can execute 👍
- then Right click the file and click `Run it as an administrator`
- Wait 4 to 5 minutes and check the activities of Malware
