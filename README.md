# MT-AWS-VPC-Project

## Objective

The Objective of this project is to create a Virtual Private Cloud (VPC) with two subnets accompanied by additional components, including
Internet Gateway (IGW)
Network Address Translation (NAT)
Route Tables
Security Groups
Network Access Control List (ACLs)


## Step 1: Create a VPC
1.	From the VPC Dashboard in the AWS Management Console.
2.	Click Create VPC.
3.	The following details were included 
o	Name tag: MTVPC
o	IPv4 CIDR block: 10.0.0.0/16
4.	Click Create VPC.

![Screenshot (69)](https://github.com/user-attachments/assets/e09fd658-61a6-4695-a354-a9b01bea6384)

![Screenshot (68)](https://github.com/user-attachments/assets/61afc26d-d5dd-4492-9048-4bb42d3e535d)

![Screenshot (1)](https://github.com/user-attachments/assets/aa116b7a-0f74-4a93-92b8-b408ac5b3025)

![Screenshot (2)](https://github.com/user-attachments/assets/ae1f924c-e153-4337-869c-b225126d40ed)

The Purpose and importance: The Virtual Private Cloud (VPC) is a virtual network that isolates your resources in the cloud. It is a logically isolated section of the AWS cloud where you can launch resources such as EC2 instances, databases, etc.
 It allows you to define and control the network settings, including subnets, route tables, and security.
 
## Step 2: Create Subnets
1.	In the VPC Dashboard, under Subnets, click Create Subnet.
2.	Add the following subnets:
Public Subnet:(10.0.1.0/24)
o	Name tag: PublicSubnet
o	VPC: MTVPC
o	Availability Zone: Select us-east-1a).
o	IPv4 CIDR block: 10.0.1.0/24
o	Click Create Subnet.
![Screenshot (3)](https://github.com/user-attachments/assets/886a7dde-4a23-4272-8666-28a3475a2d23)

•	Purpose and Importance: A public subnet is a section of the VPC that can access the internet directly via the Internet Gateway. It hosts resources that need to be publicly accessible, like web servers, NAT Gateways, and load balancers.
Private Subnet:
o	Name tag: PrivateSubnet:  10.0.2.0/24)
o	VPC: MTVPC
o	Availability Zone: Select the same one as the public subnet 
o	IPv4 CIDR block: 10.0.2.0/24
o	Click Create Subnet.
![Screenshot (4)](https://github.com/user-attachments/assets/5b79fde9-ea90-43f0-ba5f-27fb3e1e33a5)

![Screenshot (5)](https://github.com/user-attachments/assets/316e73d0-2927-4db1-9807-e90481c543c4)

•	Purpose and important: A private subnet is a section of the VPC that cannot directly access the internet and is isolated from public access. It is used to host sensitive resources like databases or application servers that should not be publicly accessible. Internet access is managed via a NAT Gateway.

## Step 3: Configure an Internet Gateway (IGW)
1.	In the VPC Dashboard, click on Internet Gateways.
2.	Click Create Internet Gateway.
o	Name tag: MTVPC-IGW
3.	After creating, select the IGW, click Actions, and choose Attach to VPC.
4.	Select the MTVPC VPC and click Attach Internet Gateway.
![Screenshot (7)](https://github.com/user-attachments/assets/1c216a36-8580-438c-9347-f77970a64d06)

![Screenshot (9)](https://github.com/user-attachments/assets/bb2399ca-15bd-43a1-b95e-3b29701d3742)

	Purpose and Importance: The IGW is a component that allows instances in the public subnet to connect to the internet.  Without an IGW, public instances (like web servers) would be unable to communicate with the outside world. The IGW acts as a bridge between your VPC and the internet.

## Step 4: Configure Route Tables
1.	In the VPC Dashboard, click on Route Tables.
Public Route Table:
o	Click Create Route Table.
o	Name tag: PublicRouteTable
o	Click Create.
o	Select the newly created route table and click Edit routes under the Routes tab.
o	Add a new route:
	Destination: 0.0.0.0/0
	Target: Select the IGW (MTVPC-IGW).
o	Click Save changes.
o	Under the Subnet associations tab, click Edit subnet associations, select the PublicSubnet, and save.
![Screenshot (11)](https://github.com/user-attachments/assets/59632644-06dd-4233-b81b-d10e2b628ae4)

![Screenshot (12)](https://github.com/user-attachments/assets/91288441-5062-4b49-b472-dff346053bcd)

![Screenshot (16)](https://github.com/user-attachments/assets/a137d2f9-7f68-408b-9283-31580e2574ba)

![Screenshot (17)](https://github.com/user-attachments/assets/ea924794-9fd0-4da5-a75a-85075c3f52ab)

•	Purpose: Route tables control the routing of traffic within the VPC. They determine where network traffic should be directed based on destination IP addresses.
•	Importance:
o	Public Route Table: Routes public traffic to the IGW so resources in the public subnet can access the internet.
o	Private Route Table: Routes traffic to the NAT Gateway, allowing private resources to access the internet indirectly.

Private Route Table:
o	Click Create Route Table.
o	Name tag: PrivateRouteTable
o	VPC: MTVPC
o	Click Create.
o	Associate the PrivateSubnet under Subnet associations.
![Screenshot (18)](https://github.com/user-attachments/assets/9b815f24-92a5-4b48-89bc-554dbc90d585)

![Screenshot (19)](https://github.com/user-attachments/assets/09baee7b-254b-47ef-b6d4-62b7fc52889c)

## Step 5: Configure a NAT Gateway
1.	In the VPC Dashboard, click on NAT Gateways.
2.	Click Create NAT Gateway.
3.	Subnet: Select the PublicSubnet.
4. 	Elastic IP allocation: Click Allocate Elastic IP and select the allocated IP.
4	After creation, go back to the PrivateRouteTable.
6	Under the Routes tab, click Edit routes.
7	Add a new route:
8	Destination: 0.0.0.0/0
9.Target: Select the created NAT Gateway.
![Screenshot (24)](https://github.com/user-attachments/assets/19f9b637-1a7a-406a-9f82-7e1577cf7803)

![Screenshot (26)](https://github.com/user-attachments/assets/6bbd5766-22af-421d-9811-e38b03f863b1)

![Screenshot (27)](https://github.com/user-attachments/assets/88376e5f-d4ea-49df-ba4d-02d67958ccd8)

![Screenshot (28)](https://github.com/user-attachments/assets/27b2272b-f1a7-4c06-9451-8f999a87a769)

•	Purpose: A NAT (Network Address Translation) Gateway allows instances in a private subnet to initiate outbound connections to the internet while remaining unreachable from the internet.  It enables resources in the private subnet (like databases) to receive updates, download patches, and connect to external services securely without exposing them to direct internet traffic.

## Step 6: Set Up Security Groups
1.	In the VPC Dashboard, click on Security Groups.
Public Instances Security Group:
o	Click Create security group.
o	Name tag: PublicSG
o	VPC: MTVPC
o	Add inbound rules:
	Type: HTTP, Port: 80, Source: 0.0.0.0/0
	Type: HTTPS, Port: 443, Source: 0.0.0.0/0
	Type: SSH, Port: 22, Source: My IP 
o	Allow all outbound traffic
![Screenshot (29)](https://github.com/user-attachments/assets/a7fbabd7-7bd5-46e5-ad78-6e045f4310d9)

![Screenshot (30)](https://github.com/user-attachments/assets/57689288-0d99-4a35-827e-b27ccea03c01)

![Screenshot (31)](https://github.com/user-attachments/assets/7f0a1e27-b29b-420f-9cb6-08454ddbfabe)

Private Instances Security Group:
o	Name tag: PrivateSubnet
o	VPC: MTVPC
o	Add inbound rules:
	Type: MySQL/Aurora, Port: 3306, Source: PublicSubnet security group.
	Type: SSH, Port: 22, Source: My IP.
o	Allow all outbound traffic. 
![Screenshot (65)](https://github.com/user-attachments/assets/32bc2362-d188-4cb8-941a-2b72195656e6)

![Screenshot (64)](https://github.com/user-attachments/assets/70067938-6ab1-40bb-84b2-4efbf4cb5349)

•	Purpose: Security groups act as virtual firewalls that control inbound and outbound traffic for resources in the VPC.
•	Importance:
o	Public Security Group: Allows HTTP, HTTPS, and SSH access from the internet to instances in the public subnet (like web servers).
o	Private Security Group: Controls traffic between public and private resources (e.g., allowing only the web servers to communicate with the database). It restricts external access, ensuring the private instances are secure.

## Step 7: Configure Network ACLs (NACLs)
Public Subnet NACL:
o	Create a new NACL named PublicNACL and associate it with PublicSubnet.
o	Add the following inbound rules:
	Rule 100: HTTP (80), Source: 0.0.0.0/0, Allow
	Rule 110: HTTPS (443), Source: 0.0.0.0/0, Allow
	Rule 120: SSH (22), Source: My IP, Allow
o	Outbound rule: Allow all traffic.
![Screenshot (34)](https://github.com/user-attachments/assets/5d7be6f6-f850-4eb3-91f8-b0ba6d3322c2)

Private Subnet NACL:
o	Create a new NACL named PrivateNACL and associate it with PrivateSubnet.
o	Add the following inbound rules:
	Rule 100: Allow traffic from PublicSubnet.
o	Add outbound rules:
	Rule 100: Allow traffic to the public subnet.
	Rule 110: Allow traffic to the internet.
![Screenshot (48)](https://github.com/user-attachments/assets/02cc0de9-565b-4a04-a836-1452d92f9d7a)

![Screenshot (66)](https://github.com/user-attachments/assets/e30ca6bf-5fa5-4c3c-9c13-a09ac5c34d0e)

![Screenshot (67)](https://github.com/user-attachments/assets/a0f06f0f-0397-43fa-b6a6-e66f5b244421)

•	Purpose: NACLs provide an additional layer of security at the subnet level by controlling inbound and outbound traffic.
•	Importance:
o	Public Subnet NACL: Allows necessary inbound protocols (HTTP, HTTPS, SSH) for resources in the public subnet while controlling outbound traffic.
o	Private Subnet NACL: Manages internal traffic between subnets and allows outbound traffic for services like database updates while blocking unauthorized access.

# Configuration of EC2 Instance 
## Public Instance
![Screenshot (50)](https://github.com/user-attachments/assets/53dbd797-3f92-449b-b608-e1319f5dd040)

![Screenshot (51)](https://github.com/user-attachments/assets/54ca7c48-6ee7-43e9-8f60-1e4f4756f00f)

![Screenshot (52)](https://github.com/user-attachments/assets/c52fc6e3-3f88-429f-bec2-1af97303dd9e)

![Screenshot (60)](https://github.com/user-attachments/assets/c34eda28-c266-4596-beb1-12c2ee28a141)

![Screenshot (54)](https://github.com/user-attachments/assets/80c9542c-17d0-43f6-8cac-1160ea71ad99)

## Private Instance
![Screenshot (55)](https://github.com/user-attachments/assets/9055851d-0f55-4cd3-b1f9-c632a18d921e)

![Screenshot (57)](https://github.com/user-attachments/assets/efa33dfb-8fdc-437c-99e0-4faf84561f81)

![Screenshot (58)](https://github.com/user-attachments/assets/6be38312-10cf-47c1-ae1e-2b8d705a7842)

![Screenshot (59)](https://github.com/user-attachments/assets/f0967336-ad33-4206-a435-d4c4e6fdebb4)

# VPC architecture
![download](https://github.com/user-attachments/assets/544b1d57-dbed-46a5-8724-e56ef5d9a7f5)
