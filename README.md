# HANDS ON DYNAMIC ANALYSIS 🧑‍💻

Download the following
- Any one malware sample https://zeltser.com/malware-sample-sources/
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

- Now, Go to files Extract the malware sample you downloaded 
- Rename it to (filename`.exe`) exe means it can execute 👍
- then Right click the file and click `Run it as an administrator`
- Wait 4 to 5 minutes and check the activities of Malware

# Investigation of process activities 🔍

 Open "Wireshark"  and "process hacker" and capture the activities by clicking those buttons👇

 <img src="https://github.com/Tripati3000/dynamic-ANALYSIS/assets/160244601/b4defeb8-7cc1-45b4-8942-be7538078798" height="80%" width="80%" alt="SIEM System steps"/>

 Click to the "Process tree" on process hacker 👇

 <img src="https://github.com/Tripati3000/dynamic-ANALYSIS/assets/160244601/625c2ea3-1654-49fa-8860-3c59013430c0" height="80%" width="80%" alt="SIEM System steps"/>




 

  # Mark the points 
  we have to find processes of malware activities like you can see here or catch any thing that looks like malware
 As we can see that Malware processes running `powershell``conhost``schtasks.exe` it means if malware starts processing a task scheduler which is schtasks.exe then it will download another malware at certain conditions were if we try to delete it then it will download again and hide itself this is called **PERSISTENCE**
 - when a new process created you can see its under in which the process is running were ( new process called child process and the process under the process created called parent process)

 <img src="https://github.com/Tripati3000/dynamic-ANALYSIS/assets/160244601/7fb6c306-4909-45ec-b84d-bbaa9b53b333" height="80%" width="80%" alt="SIEM System steps"/>


 

 # Mark the points
Open up your windows task scheduler >>> Updates 👍 you can see that new malware🔍 for more Double click it Go to Triggers you see ( at log on ) and Go to actions you see ( Start a program ) 
You can see in the screenshot that the malicious software named “VbxFiQYCyFDgGL.exe” prepared by the attacker will run when this scheduled task runs.

This is how we have detected the scheduled task that the attacker added.
 
 <img src="https://github.com/Tripati3000/dynamic-ANALYSIS/assets/160244601/57694ea2-a6b2-4606-839b-94c7495c92ea" height="80%" width="80%" alt="SIEM System steps"/>

 
<img src="https://github.com/Tripati3000/dynamic-ANALYSIS/assets/160244601/33c6f06f-3abd-41a6-bdd2-ded5163ebbd6" height="80%" width="80%" alt="SIEM System steps"/>


# Investigation of Network Activities 🔍

We have to investigate that the malware which steals our data transfer to which author by these networks (sometime it works sometimes its not)

**Open Wireshark 🦈 And here we need to search for 3 things :**
- SMTP (simple mail transfer protocol) `email`
- http (hypertext transfer protocol) `website`
- DNS (domain name system) `server`
<img src="https://github.com/Tripati3000/dynamic-ANALYSIS/assets/160244601/6ae154d8-681c-4fbe-afc4-0dd1c353aebc" height="80%" width="80%" alt="SIEM System steps"/>
<img src="https://github.com/Tripati3000/dynamic-ANALYSIS/assets/160244601/656ca414-3334-4c79-aa3c-78e4bb27a287" height="80%" width="80%" alt="SIEM System steps"/>

**You can see that it have a DNS server and querying domain 5gw4d.xyz which is suspicious 👍 and lets track the domain by its IP address ( you can copy the ip address in Destination sectiom**

<img src="https://github.com/Tripati3000/dynamic-ANALYSIS/assets/160244601/b3d98b17-2183-4e6a-83da-d049175ffe90" height="80%" width="80%" alt="SIEM System steps"/>

Paste the Ip address here - https://ip-geolocation.whoisxmlapi.com/api
Or you can use - https://www.abuseipdb.com/

# Investigation of Registry 🔍

Registries in Windows are like organized storage areas for important system and application settings. Attackers can exploit them to sneak in malicious software and make it start up whenever the computer boots, helping them steal data and maintain control over the system.

Open **Regshot** and click **2nd shot** Because we want to compare 1st shot and 2nd shot like before malware amd after malware what things have done in our virtual box 👍 after that click "compare" down below 2nd shot

<img src="https://github.com/Tripati3000/dynamic-ANALYSIS/assets/160244601/22d5fa87-7649-4d26-b510-e8cdec8fded2" height="80%" width="80%" alt="SIEM System steps"/>

**Open up regshot and find these keywords :**

- HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run

- HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunOnce

- HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Run

- HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunOnce

when the operating system started windows keep application running so resgistry means the data storage of any specific apps the user uses and thats taken advantage by the attackers and adding their own malicious registry keys

When we look at the registry, 
For example
- we check a specific area called "XYZ\Software\WOW3452Node\Microsoft\Windows\CurrrentVersion\Uninstall." Here, applications leave behind information about how they can be uninstalled. Attackers sometimes install their own software and hide it here. So, it's smart to check this area to find any sneaky apps installed by attackers.


# Investigation of file activities 🔍

**we can analyse it by two ways**

The malware files can be located in these:

- Type `Windows + R`
- 
- <img src="https://github.com/Tripati3000/dynamic-ANALYSIS/assets/160244601/2f9c1d21-7437-4478-95fd-bb79f11ff450" height="80%" width="80%" alt="SIEM System steps"/>

- Search `%temp%` (if it not have then try these two)
- `shell:startup`
               or
          `shell:common startup`
  
  <img src="https://github.com/Tripati3000/dynamic-ANALYSIS/assets/160244601/22d5fa87-7649-4d26-b510-e8cdec8fded2" height="80%" width="80%" alt="SIEM System steps"/>

- Or you can use procmon by finding 
- `C:\Users\Username\Appdata\Roaming\directory` Have under an `.exe` file
- Or `C:\Users\Username\Appdata\Roaming\logdata`
To find these go to procomon >>> process tree >>> right click the malware.exe file >>> Add process and children to include filter

<img src="https://github.com/Tripati3000/dynamic-ANALYSIS/assets/160244601/8a6af217-af68-4255-89dc-38c756daa805" height="80%" width="80%" alt="SIEM System steps"/>

Now you can see only file activities of malware 👍 in which we cannot find such activities running 😅

<img src="https://github.com/Tripati3000/dynamic-ANALYSIS/assets/160244601/1589646b-11e7-4f3f-ade8-3a6b0dddf54c" height="80%" width="80%" alt="SIEM System steps"/>

# Investigation results

-  It query to the DNS server 5gw4d.xyz✅
-  After Execution of malware it runs a file VbxFiQYCyFDgGL.exe✅
-  The malware runs `powershell``conhost``schtasks`✅
-  It uses registry keys to steal data✅
-  It uses persistence✅
