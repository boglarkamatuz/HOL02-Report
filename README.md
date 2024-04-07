# **HOL02-Report**
_Levian Gonzalez, Boglarka Matuz_

## Overview
This report provides a detailed overview of the proposed hybrid infrastructure for Project HOL02 on AWS. The infrastructure consists of a Virtual Private Cloud (VPC) segmented into three subnets: Production, Research, and DMZ. Each subnet hosts specific services and is secured with appropriate security groups.


### 0. Prerequisites
Generate key named HOL02 and import it

![keygen](images/keygen.JPG)

![key_import](images/key_import.JPG)

### 1. Configure all the AWS resources mentioned in the architecture diagram

**1.1 Virtual Private Cloud (VPC)** 

_The Virtual Private Cloud (VPC) serves as the foundation of our AWS infrastructure, providing isolated network resources for our services. The chosen CIDR block (10.0.0.0/16) allows for ample IP address space for future scalability._

**Create VPC**

![vpc](images/vpc_1.jpg)
![vpc_create](images/vpc_create.JPG)

**1.2 Create subnets**

_Using different availability zones, so if one of them is down, we can still use the others. Also using different ranges._

![subnet_DMZ](images/subnet_DMZ.JPG)
![subnet_Production](images/subnet_Production.JPG)
![subnet_Research](images/subnet_Research.JPG)

_All the subnets listed:_
![subnets_all](images/subnets_all.JPG)

**1.3 Create Internet Gateway**

_The purpose is connect the routing tables to the internet_

_Create and attach to VPC_

![IGW](images/internet_gateway.JPG)
![IGW_VPC](images/IGW_VPC.JPG)

**1.4 Configure Routing Tables**

_Now the internet gateway is established, but it is still disconnected. Routing tables are needed, so that subnets are able to access the internet_

Create routing tables for each subnet and create associations:

_(The exact example of DMZ)_

![RT_DMZ](images/RT_DMZ.JPG)
![RT_association_DMZ](images/RT_association_DMZ.JPG)
![RT_editroute_DMZ](images/RT_editroute_DMZ.JPG)

After following these steps for each subnet, the connection is shown on the resource map:

![RT_resourcemap](images/RT_resourcemap.JPG)

**1.5 Security Groups & EC2 instances**

_Security groups are created during launching the instances_

_**HOL02-VPN**_

Extra steps are taken to associate elastic IP with instance

![LI_VPN](images/LI_VPN_DMZ_1.JPG)
![LI_VPN](images/LI_VPN_DMZ_2.JPG)
![LI_VPN](images/LI_VPN_DMZ_3.JPG)
![LI_VPN](images/LI_VPN_DMZ_4.JPG)
![LI_VPN](images/LI_elasticIP.JPG)


_**HOL02-VoilaServer**_

Extra steps are taken to only accept inbound traffic from HOL02-DMZ-SG through port 22(SSH)

![LI_VPN](images/LI_Vol_Prod_1.JPG)
![LI_VPN](images/LI_Vol_Prod_2.JPG)
![LI_VPN](images/LI_Vol_Prod_3.JPG)
![LI_VPN](images/LI_Vol_Prod_4.JPG)


_**HOL02-Jupyter**_

Extra steps are taken to only accept inbound traffic from HOL02-DMZ-SG through port 22(SSH) and port 8888(TCP)

![LI_VPN](images/LI_Jup_Res_1.JPG)
![LI_VPN](images/LI_Jup_Res_2.JPG)
![LI_VPN](images/LI_Jup_Res_3.JPG)
![LI_VPN](images/LI_Jup_Res_4.JPG)


**1.6 S3 Buckets**

_Create S3 bucket_

When trying to create the bucket with the expected naming "HOL02-Notebooks" an error has been encountered. To resolve lower case letters were used and also our initials with versioning to have a unique bucket name.

![S3](images/S3_1.JPG)
![S3](images/S3_2.JPG)
![S3](images/S3_3.JPG)


### 2. Create a Jupyter Notebook named hol02-app.ipynb and upload it to the S3 bucket
 
![S3](images/S3_4.JPG)


### 3. OpenVPN Configuration

The steps provided were followed to install OpenVPN on the HOL02-VPN instance

![openvpn](images/openvpn_1.JPG)
![openvpn](images/openvpn_2.JPG)
![openvpn](images/openvpn_3.JPG)
![openvpn](images/openvpn_4.JPG)

After installation, we navigated to https://3.229.85.43:943/admin and logged in

![openvpn](images/openvpn_5.JPG)
![openvpn](images/openvpn_6.JPG)

Once logged in, in the VPN Settings and changed the hostname to the elastic IP

![openvpn](images/openvpn_7.JPG)
![openvpn](images/openvpn_8.JPG)

Then subnets were added and "Should client Internet traffic be routed through the VPN?" was set to "No"

![openvpn](images/openvpn_9.JPG)

**Installing the OpenVPN client**

![openvpn](images/openvpn_10.JPG)


### 4. Nginx Configuration

The commands provided were followed to install Nginx on the EC2 instance named HOL02-VoilaServer:
 
![nginx](images/nginx_0.JPG)
![nginx](images/nginx_1.JPG)
![nginx](images/nginx_2.JPG)


### 5. Jupyter Configuration

For the installation of python the steps shown in class were followed. 

_(1. vi install.sh and using the code that was shared_
_2. 2. bash install.sh)_

_Then using pip install jupyter, to install jupyer as well._

The following steps show the configuration:

![jupconfig](images/jup_config_1.JPG)
![jupconfig](images/jup_config_2.JPG)
![jupconfig](images/jup_config_3.JPG)
![jupconfig](images/jup_config_4.JPG)


### 6. Synchronization

To set up a cron job to synchronize files from an EC2 instance to an S3 bucket, firstly _awscli_ packge was installed.

_connection to HOL02-Jupyter isntance_

![sync](sync_jup_1.JPG)





