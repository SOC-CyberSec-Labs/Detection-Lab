# Detection-Lab

## Objective

The Detection Lab project aimed to establish a controlled environment for simulating and detecting cyber attacks. The primary focus was to ingest and analyze logs within a Security Information and Event Management (SIEM) system, generating test telemetry to mimic real-world attack scenarios. This hands-on experience was designed to deepen understanding of network security, attack patterns, and defensive strategies.

### Skills Learned

- Advanced understanding of SIEM concepts and practical application.
- Proficiency in analyzing and interpreting network logs.
- Ability to generate and recognize attack signatures and patterns.
- Enhanced knowledge of network protocols and security vulnerabilities.
- Development of critical thinking and problem-solving skills in cybersecurity.

### Tools Used

- Security Information and Event Management (SIEM) system for log ingestion and analysis.
- Network analysis tools (such as Wireshark) for capturing and examining network traffic.
- Telemetry generation tools to create realistic network traffic and attack scenarios.

## Network Diagram

Before configuring our virtual machines, we want to create a network diagram of our lab network.

## Getting Started
VirtualBox will be used for the virtual machines in our lab. We'll need Windows 10 installed as a virtual machine in VirtualBox and Kali Linux as well. We'll also want to install Splunk and Sysmon on our Windows 10 machine.

<div><img width="329" height="100" alt="VBoxSnapshotW10" src="https://github.com/user-attachments/assets/ac15936b-90ca-45db-82fb-6c4ac41af3a6" /></div>
<i>Window 10 Virtual Machine in VirtualBox with a snapshot after Splunk installation</i>

We can make a snapshot of our machine before installing any software or executing any malware in a sandbox environment to revert changes, if necessary.

## Configuring Virtual Machines
<div><img width="781" height="518" alt="VBoxNetworkSettings" src="https://github.com/user-attachments/assets/5e2578d5-8d1e-4a79-8884-6db0ee64273d" /></div>
<i>VBox Network Setting for Internal Network</i>

To reduce the risk of compromising our home network when testing malware, we want to change our network settings in VirtualBox for the relevant VMs from NAT to Internal Network. This will keep the VMs off the internet and in their own private VLAN.

<div>
  <img width="1126" height="637" alt="Windows10StaticIP" src="https://github.com/user-attachments/assets/02584660-ffa6-487c-a7a6-1b0de3857b6c" />
  <i>Static IP configuration for Windows 10 target machine</i>
  <img width="1322" height="554" alt="KaliLinuxStaticIP" src="https://github.com/user-attachments/assets/9b36b3ef-1e62-4cfe-872f-6b1ffcb8d0fb" />
  <i>Static IP configuration for Kali Linux attack machine</i>
</div>

Next, we can configure our IP to static. The IP address can be whatever you prefer, as long as they are in the same subnet.

## Setting up Malware
To run our exploit on the target machine, we have to disable real-time protection.
<div>
  <img width="593" height="342" alt="Windows10DisableRTProtection" src="https://github.com/user-attachments/assets/8a424115-f057-4d4e-acf6-94569049a2fb" />
</div>
Then we enable Remote Desktop Protocol on the target machine.
<div>
  <img width="804" height="636" alt="Windows10EnableRDP" src="https://github.com/user-attachments/assets/8f64d7dd-725c-470c-ae27-bd233c676240" />
</div>

We'll do a network scan of our target machine to find open ports. We see that port 3389 for Remote Desktop Services (RDP) is open.

<img width="851" height="582" alt="Kali_nmap_RDP" src="https://github.com/user-attachments/assets/15dfd49c-60c4-4d43-8b32-2117df87bddf" />

Let's run msfvenom in Kali Linux to create our malware executable. We'll configure the executable to connect to our attackbox.

<img width="886" height="266" alt="MalwareExecutableCreation" src="https://github.com/user-attachments/assets/2ce88d67-c46a-4236-8adc-c70e9fb1d5f1" />

Launch metasploit and run the handler to set our payload then run our handler to listen in on our exploit.

<div>
  <img width="573" height="33" alt="msfconsole_startup_command" src="https://github.com/user-attachments/assets/71293191-5c71-43b9-9d08-84c1be90a30f" />
</div>
<i>msfvenom console start command</i>

<div>
  <img width="463" height="50" alt="metasploit_handler_command" src="https://github.com/user-attachments/assets/5315d6ed-e532-49f0-8caa-c8fc30dbb917" />
</div>
<i>Select our exploit handler with the use command</i>

<div>
  <img width="696" height="32" alt="msf_handler_setPayload" src="https://github.com/user-attachments/assets/41621293-625f-4cd8-8229-d955384c2d70" />
</div>
<i>Set the payload of our malware to reverse TCP</i>

<div>
  <img width="787" height="291" alt="msf_handler_set_lhost_options" src="https://github.com/user-attachments/assets/b4e6513d-ebde-4a22-809a-eab7d0e5b33f" />
</div>
<i>Next, we can set the listening host of our exploit to the attack machine.</i>





*python3 server*
We can server the malware on our local network easily with a simple python 3 server.

## Executing Malware
*downloading file on Target machine*
Now, we can simply visit the server on our target machine and download the malware executable.


*Running the malware*
Then, we can run it.

## Examining Telemetry with Splunk

*splunk index = endpoint*
Now that we've launched our malware, we can view the logs created in Windows with Splunk.


