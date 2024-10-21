![image](https://github.com/user-attachments/assets/cf328dc2-28da-4fae-877e-7586bd50cd04)
# OPNsense_Firewall   

![image](https://github.com/user-attachments/assets/b6bda4b9-42f5-4d78-b256-291c380cec30)
## Suricata IDS/IPS installation & Configuration 


Description:  This is an instruction on how to install and configure the Suricata IDS/IPS on the Opensense open-source firewall running on the VirtualBox lab environment. 

Note: this instruction is written based on Opensense version 24.7 

## Setting up and Configuring Suricata

1. Before installing and configuring, run Kali Linux and access the Opensense web UI on its LAN address.  
navigate to Interfaces > Settings and unselect the following "Network Interfaces" features as Opensense recommends.  
	
![image](https://github.com/user-attachments/assets/04792d71-e467-4834-ac68-1418993ef38b)

2. Navigate to Services > Intrusion Detection > Administration and select the following features of IPS
    
 - Advanced Mode: ON
 - Enabled: enabled
 - IPS Mode: enabled
 - Promiscuous mode: enabled
-  Enable Syslog alerts: enabled
  -  Pattern matcher: Hyperscan   ( Hyperscan is a more optimised pattern matching  technique giving us a better performance boost)
  - Detect Profile: Medium
  - Interfaces: LAN ( for labs; otherwise, both LAN and WAN can be selected)
  - Home Networks: < the LAN network subnet>

3. On the Download page, an extensive list of detection rules can be enabled depending on your use case. 
![image](https://github.com/user-attachments/assets/e13dabeb-b402-4aee-b415-8713628a6064)

4. However, you can create custom rules using the " Snorpy- http://www.cyb3rs3c.net/" web-based rule creator tool. This can be used for both Snort and Suricata IDS/IPS.
   ![image](https://github.com/user-attachments/assets/8820148d-db22-43d7-9268-39d548ef4823)

5. Enable the Secure Shell for transferring custom rule files to the firewall, navigate to System > Administration> Secure Shell and enable the 'Secure Shell server', 'root login', and' Auth method' and only allow accepting a connection on![image]
![image](https://github.com/user-attachments/assets/1366c14f-097f-480d-b81c-1c45f7e1d50f)

6. Once a custom rule file is created, we need to create an XML file instructing Opensense where to download the rule file, as shown below.
   ![image](https://github.com/user-attachments/assets/f39a99b0-4d8c-49f8-887a-06e9dcae291e)

7. Both .rule and .xml files must be uploaded onto the " usr/local/ Opensense/scripts/Suricata/metadata/rules" directory using a file transfer tool like Filezilla.
8. Navigate to Services > Intrusion Detection > Administration and refresh the download rule page. 
9. Select the custom rule and click on "Enabled selected". Once done, select " Download & Upload Rules. 
Note: you need to set up an HTTP server on Kali to receive a GET request from the firewall to grab the custom rule file.
10. If successful, the upload date and time will appear under "Last update", and a new custom rule will be populated under the 'Rules' tab.

![image](https://github.com/user-attachments/assets/7ba65c85-1abe-40a9-90ba-3f6c80be69b7)



## Testing Suricata IDS/IPS 

1. Navigate back to Kali
2. Run stealth scan command from Nmap : sudo nmap -sS -Pn --top-ports 500 < firewall IP >
3. Check the 'Alerts' tab once the scan is complete. 
	
![image](https://github.com/user-attachments/assets/85bcb0c0-fe90-441e-88f2-0b8cdb6ac031)






