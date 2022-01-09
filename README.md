# SNOW-Discovery-MID-Server
- Discovery application in SeviceNow finds computers, servers, and network enabled devices like routers and the applications that tun on them.
- Populates the data in the CMDB after validation
- Updates the hardware and software data and dependencies
- Discovery is an agentless product of ServiceNow- we don't have to install agents on external servers

## Why do we need Discovery?
- Everithing is manual , to automate we need discovery

![image](https://user-images.githubusercontent.com/12488769/148691106-947db020-ef17-428a-9aae-3a3a047d3121.png)

- Discovery makes it easy to automate the CI population into ServiceNow CMDB
![image](https://user-images.githubusercontent.com/12488769/148691145-81f830f2-d10e-46bb-bd5a-33e7d40b9ed0.png)

## When you don't use Discovery
- data quality might be compromised
- dependent on multiple sources
- failure of imports or process of importing data into cmdb

## Discovery Architecture
![image](https://user-images.githubusercontent.com/12488769/148691200-d5733799-d3c9-4fea-9655-5f30061c087e.png)

## Discovery Components
- probes
- sensors
- patterns

## Probes and Sensors
- probe collects the information
- sensor processes the information collected by probe
- both get instructions via ECC queue
- Worker job on the MID Server monitors the queue for work

## Patterns
- Similar to probes and sensors
- Series of operations that also collect data on a host, process it, and update the CMDB
- Neebula Discobery Language (NDL)
- Pattern Designer
- Scripting is differen since it uses NDL
- we can customize our own patterns using pattern designer

## 2 Types of Discover
- Horizontal
![image](https://user-images.githubusercontent.com/12488769/148691413-18d5b712-5ee9-4bf7-a056-c209c226094b.png)
Doesn’t create Relationship between CI’s and dependencies, which is done by Service Mapping.
![image](https://user-images.githubusercontent.com/12488769/148691420-92b50bf2-8438-486d-be2d-c943680e1971.png)


- Top-down Service Mapping
![image](https://user-images.githubusercontent.com/12488769/148691441-94a1c31e-74f4-4a0f-bddb-359852d0214e.png)
Create Relationship between CI’s and dependencies![image](https://user-images.githubusercontent.com/12488769/148691447-96b56043-c50d-4ef2-8dc2-10878d6fb1ca.png)

# MID Server
- ECC Queue
- ECC Queue Process Flow
-How to Install and Setup the MID Server!
## What is MID Server?
- MID Server is a Java application that runs as a Windows service or UNIX daemon on a server in your local network.
-  The MID Server enables communication and the movement of data between a ServiceNow instance and external applications, data sources and services.
-  For example: ServiceNow can’t communicate with Internal applications of the Company because access is limited on the Network and therefore MID Server comes into the picture.
-  MID Server needs be installed into the Internal Network of the company and then ServiceNow can communicate with internal network via MID Server.
![image](https://user-images.githubusercontent.com/12488769/148691618-3fb3ad5c-3719-4333-a76f-1dcb155d728f.png)

## How ServiceNow Communicates with MID Server
- Perform configuration on MID Server where we need to put some details of ServiceNow with UserName and Password so that MID server has access to the ServiceNow instance, and they can also do Handshake.
![image](https://user-images.githubusercontent.com/12488769/148691647-623a5e62-3017-4f95-8669-19ac7b02dc34.png)

## Applications and MID Server
![image](https://user-images.githubusercontent.com/12488769/148691662-0093c513-f8d0-4703-8507-9d26648d57cf.png)

## External Communication Channel
- Connection point between Instance and MID Server
- ECC Queue is a table of records which stores information sent from ServiceNow to another system and from another System to ServiceNow
- ECC Queue record is a message sent from serviceNow or incoming message from a 3rd party system

## How MID Server usess ECC Queue
- MID Server always communicate with instance via Worker Job and checks for new Output messages.
ECC Queue stores all Input and Output messages to take appropriate actions
![image](https://user-images.githubusercontent.com/12488769/148691784-c597f081-6ff7-42bf-9869-f407fff2ee8a.png)

## ECC Queue Process Flow
- Once New message is created in ECC Queue and then System checks whether it is Input or Output message. If it is Output message, then State becomes Ready 
![image](https://user-images.githubusercontent.com/12488769/148691805-6a9b41e3-567d-48dc-ad58-a5a7ead8e24d.png)





# Install & setup a MID Server

##
1. Create MID Server User
- Create a new user on sys_user Table and provide ‘mid_server’ role.
![image](https://user-images.githubusercontent.com/12488769/147857692-96377755-5c16-448e-96c2-2a69df38166e.png)

2.  Get a Windows or Linux SERVER
- Install Virtual Client Software as per below:
 - For MAC – VMWare Fusion
 - For Windows – VMware Workstation      (https://www.vmware.com/products/workstation-player.html)
- Download Windows Server ISO File and use it in your VM installed
(https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2022)
- Complete Windows Server 2022 installation process in the Virtual Machine.
![image](https://user-images.githubusercontent.com/12488769/147857710-e4c241f4-8cf9-4480-8384-2cdfa818c815.png)

3. Download MID Server
Download MID Server ZIP file from ServiceNow instance on the Virtual Machine as per the Operating System and Extract All.
![image](https://user-images.githubusercontent.com/12488769/147857730-b40e60fe-9581-447f-bdfd-c08005a27fc1.png)

4. Install MID Server

5. Validate MID Server

7. Activate Discovery
- Discovery application can be enabled with the help of ServiceNow  HI Portal
- Has Subscription fee
- Part of ITOM standard package

8. Run a quick discovery
![image](https://user-images.githubusercontent.com/12488769/147888250-a368b590-ae1f-42a3-984d-04f88aeb5227.png)
