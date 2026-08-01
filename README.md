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
  <img width="978" height="511" alt="Windows10StaticIPConfirm" src="https://github.com/user-attachments/assets/924dfeb5-8cd0-4611-9170-c1c44ac28bbd" />
</div>



*configuring static IP and Subnet of VMs*
Next, we can configure our IP and Subnet to static. The IP address can be whatever you prefer, as long as they are in the same subnet.

## Setting up Malware
*nmap in Kali Linux*
We'll do a network scan of our target machine to find open ports. We see that port 3389 for Remote Desktop Services (RDP) is open.

*metasploit in Linux*
Let's run msfvenom in Kali Linux to create our malware executable. We'll configure the executable to connect to our attackbox.

*metasploit handler in Linux*
Launch metasploit and run the handler to set our payload and run our handler to listen in on our exploit.

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


