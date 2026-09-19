\#   AWS Custom VPC Network Infrastructure \& EC2 Deployment



\##  Project Overview

This project demonstrates designing and provisioning a custom, isolated AWS Virtual Private Cloud (VPC) network infrastructure using the AWS Management Console. It covers creating Public and Private Subnets across Availability Zones, configuring an Internet Gateway (IGW) for public connectivity, setting up custom Route Tables, and deploying/verifying an Ubuntu EC2 instance within the custom network environment.



\---



\##  Network Architecture \& Specifications

\* \*\*VPC CIDR Block:\*\* `10.0.0.0/16`

\* \*\*Public Subnet:\*\* `10.0.1.0/24` (Associated with Internet Gateway \& Public Route Table)

\* \*\*Private Subnet:\*\* `10.0.2.0/24` (Isolated internal network)

\* \*\*Internet Gateway (IGW):\*\* Attached to `Custom-VPC` for outbound/inbound public routing.

\* \*\*Compute Instance:\*\* Ubuntu 24.04 LTS deployed inside `Public-Subnet`.



\---



\##  Step-by-Step Implementation



\### 1. Custom VPC \& Subnet Provisioning

\* Created an isolated Virtual Private Cloud (`Custom-VPC`) with a `/16` IPv4 CIDR range.

\* Defined dual subnets:

&#x20; \* \*\*Public Subnet (`10.0.1.0/24`)\*\*: Configured with auto-assign public IPv4 enabled for public-facing assets.

&#x20; \* \*\*Private Subnet (`10.0.2.0/24`)\*\*: Isolated subnet for private resources.



\### 2. Internet Gateway \& Route Table Setup

\* Provisioned and attached an Internet Gateway (`Custom-IGW`) to the VPC.

\* Configured a custom Route Table (`Public-RT`) with a default route (`0.0.0.0/0`) pointing to the Internet Gateway.

\* Associated the Public Route Table with the Public Subnet to grant external network connectivity.



\### 3. Compute Deployment \& SSH Connectivity

\* Launched an EC2 instance (`VPC\_TEST`) inside the newly created `Custom-VPC` and `Public-Subnet`.

\* Configured Security Group inbound rules allowing SSH (`TCP 22`) traffic.

\* Secured private key permissions on AWS CloudShell and established a successful SSH session:

```bash

chmod 400 Key1.pem

ssh -i Key1.pem ubuntu@16.16.68.215



\##  Architecture Verification



|Component / Step|Description|Screenshot|
|-|-|-|
|VPC \& Subnets Setup|Visual representation of VPC, Subnets, and IGW linkage|\[VPC Wizard Overview](screenshots/vpc-wizard.png)|
|EC2 Launch \& Networking|Verification of EC2 instance running inside Custom VPC|\[EC2 in Custom VPC](screenshots/ec2-launch.png)|
|SSH Access \& Verification|Successful SSH connection to EC2 via AWS CloudShell|\[SSH Connection Success](screenshots/ssh-success.png)|



&#x20;###Security \& Networking Best Practices

&#x20;      \*     Network Isolation: Isolated public traffic from private components using dual-subnet architecture.



&#x20;      \*      Strict Permission Control: Restricted SSH private key file permissions (400) before establishing remote access.



&#x20;      \*      Key-Based Authentication: Replaced password-based authentication with RSA SSH Key Pairs.

