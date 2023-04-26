# Hypervisor ESXi 

## Overview

*Datastore*: free space, free space in %, total space, used space, used space in %. 

*Memory*: used memory, used memory %, total memory, free memory, free memory in %.

*CPU*: used cpu, used cpu %, free cpu, free cpu %.

*Network*: bytes received, bytes transmitted. 

*Graphs*: free cpu %, free memory%, host network usage.

*Triggers*: some triggers are in the *Triggers section of the Template* some are in the *Discovery List*


*ESXi UUID*


0. The link for finding the UUID of the ESXi host (https://x.x.x.x/mob/?moid=ha-host&doPath=hardware.systemInfo). 


1. If link did not work (Config.HostAgent.plugins.solo.enableMob), find this on system advanced settings, search this plugin and make it true.


2. After connecting the ESXi host to the **ZABBIX** for security reasons disable that plugin.


3. Additionaly you have to create new user and then add read-only permissions to that user in VMware ESXi.


*Host Configuration in Zabbix*

0. Import the template from Configuration=>Templates=>Import

1. Open the Configuration=>Hosts=>Create Host

2. In the Host name section add your **uuid** then in the visible name section you can write whatever you want.

3. Templates Section should be our template which imported to the system. 

4. Group could be created or you can add the host to the existed group 

5. Interfaces section choose the agent and write the **IP address** of the host.

6. Move to the macros section and add 3 macros.
{$USERNAME} -> User connect ESxi
{$PASSWORD} Password access to Esxi
{$URL} - https://ESXI /sdk


**If you have not access to the ESXI host graphically you can follow this steps in order to get necessary information:**

0. For getting uuid.bios:
<code> vim-cmd hostsvc/hostsummary | grep uuid </code>

1. For creating the user use this command:(change for your need *username* and *password*) 
<code> esxcli system account add -d "description" -i username -p password -c password </code>

2. For giving to this user read only permissions:
<code> esxcli system permission set -i "username" -r ReadOnly </code>

3. For getting system hostname if needed:
<code> esxcli system hostname get </code>

4. If it is required For getting vc.uuid: 
<code>esxcli system uuid get</code>

*P.S: In our case use **uuid.bios** for monitoring.* 
 









 
