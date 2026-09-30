# Implementing Agent Based Monitoring of a Windows 11 VM
Project detailing the deployment of a Tenable/Nessus Agent on a Windows 11 Virtual Machine in Azure. By running locally on the VM's operating system, the agent acts as an internal sensor to efficiently track vulnerabilities and configuration drift.

Primary benefits of this deployment model include:
- No Credential Management Overhead
- Drastically Reduced Network Impact & Complexity 
- Continuous Tracking of Transient Workloads
- Granular Endpoint & Compliance Visibility

---
_**Inception State:**_ No Nessus Agent installed or configured, no scan group created.   
_**Completion State:**_ Nessus Agent fully installed, agent group created, scan ran, vulnerabilities identified, and initial assessment conducted.

![Screenshot 2025-06-06 102351](https://github.com/user-attachments/assets/b18b3150-3fdd-41b8-a487-23c6531d5324)

![graphic_nessus_agent_technical_paper1](https://github.com/user-attachments/assets/1a7d14bf-377a-4f4a-94c1-50b02b6b3a79)

---

# Technology Utilized
- **Tenable** (Nessus Agent, Tenable.io Cloud platform)
- **Azure Virtual Machines** (Windows 11 Pro)
- **PowerShell** (Agent installation and configuration)
- **Tenable Agent Groups** (for grouping scan targets)

---

## 1. Provisioning Azure Virtual Machine

**To start, we'll provision a Windows 11 virtual machine in Azure:**

<img width="1000" height="800" alt="Deploying VM" src="AgentBasedMon-Windows/VM Deployed.png"/> 

---

## 2. Nessus Agent Group Creation
**Next, we'll create a new Agent Group in Tenable in order to localize the agent for our VM:**

<img width="1000" height="800" alt="Creating agent" src="AgentBasedMon-Windows/Creating Agent Group.png"/> 

---

## 3. Nessus Agent Scan Creation
**Then, we'll create a Basic Agent Scan connected to our Agent Group created in the previous step:**

<img width="1000" height="800" alt="Creating scan" src="AgentBasedMon-Windows/Creating scan.png"/> 

<img width="1000" height="800" alt="Creating scan" src="AgentBasedMon-Windows/Creating scan2.png"/> 

**Setting the scan type to `Trigger Scan`, Selecting `Filename` and then including the `start.txt`**

<img width="1000" height="800" alt="setting scan type" src="AgentBasedMon-Windows/Selecting scan type.png"/> 

---

## 4. Running Command from Tenable to intall the Agent inside the VM
**When creating a Linked Agent, Tenable provides the PowerShell command needed to initiate the installation process on the VM:**

<img width="1000" height="800" alt="provisioning agent" src="AgentBasedMon-Windows/Provisioning Tenable Agent.png"/> 

<img width="1000" height="800" alt="running command on VM" src="AgentBasedMon-Windows/Running command on VM.png"/> 

**This command downloads the PowerShell script from the Tenable server, places it in the current directory in PowerShell, and executes by connecting the key value password that lets the script know to connect to the Tenable console and lets it know it's an agent.**

<img width="1000" height="800" alt="agent installing" src="AgentBasedMon-Windows/Agent Installing.png"/> 

<img width="1000" height="800" alt="agent finished installing" src="AgentBasedMon-Windows/Agent finished installing.png"/> 

---

## 5. Creating the `start.txt` trigger file in PowerShell inside the VM:
**The Agent will detect it, use it as the trigger, and once finished, will delete the trigger file.**

<img width="1000" height="800" alt="creating trigger file" src="AgentBasedMon-Windows/Creating trigger file in PowerShell.png"/> 

**Confirming that Tenable Nessus Agent is running via Services on the VM**

<img width="1000" height="800" alt="confirming Tenable Agent is running" src="AgentBasedMon-Windows/Confirmation of Tenable Agent Running.png"/> 

---

## 6. File Deleted and Results
**After some time, the file `start.txt` was triggered and deleted from the VM**

<img width="1000" height="800" alt="confirming start.txt file deleted" src="AgentBasedMon-Windows/Start file deleted.png"/> 

**Status of scan showing `Triggered` in Tenable:**

<img width="1000" height="800" alt="scan status showing 'Triggered'" src="AgentBasedMon-Windows/Scan confirmation status.png"/> 

**...And finally, the results from the scan**

<img width="1000" height="800" alt="scan results" src="AgentBasedMon-Windows/Scan results.png"/> 
