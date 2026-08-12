# AWS VPC + EC2 Static HTML Application

## 📌 Project Overview

A beginner AWS networking project to understand:

- VPC
- Public and Private Subnets
- Route Tables
- Internet Gateway
- Security Groups
- EC2
- SSH using MobaXterm
- Ubuntu
- Nginx
- Static HTML deployment

A simple HTML application was deployed on an Ubuntu EC2 instance inside a public subnet and accessed through the Internet using the EC2 public IP.

---

## 🏗️ Architecture

```text
                    Internet
                       |
                Internet Gateway
                       |
                Public Route Table
                       |
                 Public Subnet
                  10.0.1.0/24
                       |
                    EC2
                       |
                    Nginx
                       |
                  index.html


                 Private Subnet
                  10.0.2.0/24
☁️ AWS Resources
VPC
Name: my-learning-vpc
CIDR: 10.0.0.0/16

The VPC provides the overall private network for the project.

Public Subnet
Name: public-subnet
CIDR: 10.0.1.0/24

The EC2 instance was deployed inside this subnet.

The subnet is public because its route table contains a route to the Internet Gateway.

Private Subnet
Name: private-subnet
CIDR: 10.0.2.0/24

No EC2 instance was deployed here.

This subnet was created to understand the difference between public and private subnets.

Internet Gateway
Name: my-learning-igw
VPC:  my-learning-vpc

The Internet Gateway provides Internet connectivity for resources in the public subnet.

🛣️ Route Tables
Public Route Table
Name: public-route-table

10.0.0.0/16  →  local
0.0.0.0/0    →  Internet Gateway

The public subnet is associated with this route table.

The 0.0.0.0/0 route sends Internet-bound traffic to the Internet Gateway.

Private Route Table
Name: private-route-table

10.0.0.0/16  →  local

The private subnet is associated with this route table.

There is no direct Internet Gateway route.

🖥️ EC2 Instance
AMI:        Ubuntu
Subnet:     public-subnet
Private IP: 10.0.1.151
Public IP:  43.205.191.105

The EC2 instance runs Ubuntu and hosts the HTML application using Nginx.

🔐 Security Group
Name: web-server-sg
Inbound Rules
SSH
Port: 22
Source: My IP

HTTP
Port: 80
Source: 0.0.0.0/0

SSH was restricted to my IP.

HTTP port 80 was allowed from the Internet so that the website could be accessed publicly.

🔑 SSH Access

MobaXterm was used to connect to the Ubuntu EC2 instance.

Protocol: SSH
Port:     22
Username: ubuntu
Key:      .pem
🌐 Nginx Setup
Update Ubuntu
sudo apt update
sudo apt upgrade -y
Install Nginx
sudo apt install nginx -y
Start Nginx
sudo systemctl start nginx
Enable Nginx at Boot
sudo systemctl enable nginx
Check Nginx
sudo systemctl status nginx

Expected:

Active: active (running)
🔎 Verify Port 80

Nginx was verified to be listening on port 80:

sudo ss -tulpn | grep :80

Expected:

0.0.0.0:80
[::]:80
🧪 Test Nginx Locally
curl http://localhost

This confirmed that Nginx was successfully serving the HTML application from the EC2 instance.

📄 Application

Nginx web root:

/var/www/html/

Application file:

/var/www/html/index.html
index.html
<!DOCTYPE html>
<html>
<head>
    <title>My First AWS Application</title>
</head>

<body>

    <h1>Hello World!</h1>

    <h2>
        This is me deploying my application on an EC2 instance and running it.
    </h2>

    <p>
        This application is running on an Ubuntu EC2 instance
        inside an AWS VPC.
    </p>

    <p>
        EC2 is deployed in a public subnet and the application
        is being served using Nginx.
    </p>

</body>
</html>
🌍 Application Access

The application was accessed using the EC2 public IP:

http://43.205.191.105
🔄 Traffic Flow
Browser
   ↓
Internet
   ↓
Internet Gateway
   ↓
Route Table
   ↓
Public Subnet
   ↓
EC2
   ↓
Security Group :80
   ↓
Nginx
   ↓
index.html