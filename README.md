# **HOL02-Report**
_Levian Gonzalez, Boglarka Matuz_

## Overview
This report provides a detailed overview of the proposed hybrid infrastructure for Project HOL02 on AWS. The infrastructure consists of a Virtual Private Cloud (VPC) segmented into three subnets: Production, Research, and DMZ. Each subnet hosts specific services and is secured with appropriate security groups.


### 0. Prerequisites
Generate key named HOL02 and import it

![keygen](keygen.JPG)

![key_import](key_import.JPG)

### 1. Configure all the AWS resources mentioned in the architecture diagram

**Virtual Private Cloud (VPC)** 

_The Virtual Private Cloud (VPC) serves as the foundation of our AWS infrastructure, providing isolated network resources for our services. The chosen CIDR block (10.0.0.0/16) allows for ample IP address space for future scalability._

**Create VPC**

![vpc](vpc_1.jpg)
![vpc_create](vpc_create.JPG)


