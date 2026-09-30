# Implementing Agent Based Monitoring of a Windows 11 VM
Project detailing the deployment of a Tenable/Nessus Agent on a Windows 11 Virtual Machine in Azure. 

_**Inception State:**_ No Nessus Agent installed or configured, no scan group created.

_**Completion State:**_ Nessus Agent fully installed, agent group created, scan run, vulnerabilities identified, and initial assessment conducted.

![Screenshot 2025-06-06 102351](https://github.com/user-attachments/assets/b18b3150-3fdd-41b8-a487-23c6531d5324)

![graphic_nessus_agent_technical_paper1](https://github.com/user-attachments/assets/1a7d14bf-377a-4f4a-94c1-50b02b6b3a79)

# Technology Utilized
- Tenable (Nessus Agent, Tenable.io Cloud platform)
- Azure Virtual Machines (Windows 10 Pro)
- PowerShell (Agent installation and configuration)
- Tenable Agent Groups (for grouping scan targets)

---

## 1. VM and Nessus Agent Setup

**To start, we'll provision a Windows 11 virtual machine in Azure:**

![1-Created VM](https://github.com/user-attachments/assets/eebd4c61-d000-4f7a-a6ad-49a0cb3b1065)

## 2. Nessus Agent Group Creation
**Next, we'll create a new Agent Group in Tenable in order to localize the agent for our VM:**

![2- Tenable - Settings - Sensors](https://github.com/user-attachments/assets/450c7f5a-b5ef-4a37-b57f-a55678c3138f)

![3- In Sensors page - Nessus Agents - Agents Group](https://github.com/user-attachments/assets/feb1f280-a997-4b9b-8605-e4529ee3949d)

![4- Added an Agent Group](https://github.com/user-attachments/assets/cc528698-b075-46cf-91a9-47649f84feae)

## 3. Nessus Agent Scan Creation
**Then, we'll create a Basic Agent Scan connected to our Agent Group created in the previous step:**

![5- Scans - Create Scan - Nessus Agent - Basic Agent Scan](https://github.com/user-attachments/assets/f83b88bd-6f8d-4206-9c55-05aee09df51b)

![6- Editing the Scan - Including the Group Agent](https://github.com/user-attachments/assets/8f38d4e0-d7cd-4d3e-b1d1-2812f73323c0)

**Set Scan Type to Trigger Scan, Selected Filename and then included the star.txt**

![Screenshot 2025-06-06 135533](https://github.com/user-attachments/assets/71a59913-3201-47f5-adb2-f2724ffa26f7)


## 4. Ran Command from Tenable to intall the Agent inside the VM
**Got the Command from Tenable by creating a Linked Agent, copied and pasted in Powershell inside the VM to install the Agent**

![8- Get Command from Linked Agents from Creating a new agent to run in the VM to install the Agent](https://github.com/user-attachments/assets/46a7d650-f869-4962-9584-a00291a662ba)




![9- Inside VM ran code in Powershell to Install the Agent](https://github.com/user-attachments/assets/ebede4ce-70a2-47a1-a747-a3c006fcdf4e)

This command downloads the PowerShell script from the Tenable server, places it in the current directory in PowerShell, and executes by connecting the key value password that lets the script know to connect to the Tenable console and lets it know it's an agent.



## 5. Created the file name star.txt in PowerShell inside the VM
**Used these commands to create the star.txt file so the Agent can detect, trigger and delete the file**

![10- Created the star txt file to trigger the scan](https://github.com/user-attachments/assets/14ac16db-7459-4eae-b79e-f7fe960f9837)

![11- File showing in the folder](https://github.com/user-attachments/assets/738cd3dc-8823-4d46-89d7-0b4309a586d9)

**Made sure that Tenable Nessus Agent was running in Services**
![12- Made sure the Tenable Nessus Agent was running](https://github.com/user-attachments/assets/76ca8adf-d4e2-43a4-be95-f3ac539dec20)

## 6. File Deleted and Results
**After 10 minutes the file star.txt was triggered and deleted from the VM**

![13- After 10 minutes the the file was deleted](https://github.com/user-attachments/assets/b340555f-a809-483e-85cd-0e4c16b7f3de)

**In Tenable is showing that the scan was triggered**

![14- In Scans is showing as triggered](https://github.com/user-attachments/assets/5e191783-8737-4071-93a4-c95a4be21b60)

**The Results from the Scan**

![15- Check the Results from Scan](https://github.com/user-attachments/assets/e5dffb82-a46a-424c-96cb-79c18e7a7959)
