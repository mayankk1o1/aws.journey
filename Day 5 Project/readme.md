# AWS VPC + EC2 Static HTML Application

## Overview

A beginner AWS networking project to understand VPC, subnets, route tables, Internet Gateway, Security Groups, EC2, SSH, Nginx, and deployment of a simple HTML application.

The application runs on an Ubuntu EC2 instance inside a public subnet and is accessed through the EC2 public IP.

## Architecture

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
Ubuntu EC2
10.0.1.151
   |
Nginx :80
   |
index.html

A separate private subnet was also created:

Private Subnet
10.0.2.0/24

No EC2 instance was deployed in the private subnet.

AWS Resources
VPC
Name: my-learning-vpc
CIDR: 10.0.0.0/16

Purpose: Provides the overall private AWS network.

Public Subnet
Name: public-subnet
CIDR: 10.0.1.0/24
Availability Zone: ap-south-1a
EC2 deployed here

Purpose: Hosts the Internet-facing EC2 instance.

Private Subnet
Name: private-subnet
CIDR: 10.0.2.0/24

Purpose: Used to understand private networking. No EC2 was deployed here.

Internet Gateway
Name: my-learning-igw
Attached to my-learning-vpc

Purpose: Provides Internet connectivity to the VPC.

Route Tables
Public Route Table

Name:

public-route-table

Routes:

10.0.0.0/16  -> local
0.0.0.0/0    -> Internet Gateway

The public subnet is associated with this route table.

The 0.0.0.0/0 route sends Internet-bound traffic to the Internet Gateway.

Private Route Table

Name:

private-route-table

Routes:

10.0.0.0/16  -> local

The private subnet is associated with this route table.

There is no direct Internet Gateway route.

EC2 Instance
AMI: Ubuntu
Subnet: public-subnet
Private IP: 10.0.1.151
Public IP: 43.205.191.105
Access: SSH through MobaXterm

SSH username:

ubuntu
Security Group

Name:

web-server-sg

Inbound rules:

Protocol	Port	Source	Purpose
SSH	22	My IP	SSH access
HTTP	80	0.0.0.0/0	Web access

SSH was restricted to my IP while HTTP was allowed from the Internet.

SSH Access

MobaXterm was used to connect to the Ubuntu EC2 instance.

Protocol: SSH
Port: 22
Username: ubuntu
Authentication: .pem key
Nginx Installation

Update Ubuntu:

sudo apt update
sudo apt upgrade -y

Install Nginx:

sudo apt install nginx -y

Start Nginx:

sudo systemctl start nginx

Enable Nginx at boot:

sudo systemctl enable nginx

Check status:

sudo systemctl status nginx

Expected:

Active: active (running)
Nginx Verification

Check port 80:

sudo ss -tulpn | grep :80

Expected:

0.0.0.0:80
[::]:80

Test locally:

curl http://localhost

This confirms that Nginx is serving the application.

HTML Application

Application directory:

/var/www/html/

Main file:

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
Application Access

The application was accessed through:

http://43.205.191.105

Traffic flow:

Browser
   |
Internet
   |
Internet Gateway
   |
Route Table
   |
Public Subnet
   |
EC2
   |
Security Group :80
   |
Nginx
   |
index.html
Troubleshooting

The application initially did not load from the browser.

The problem was isolated by checking each layer.

Nginx
sudo systemctl status nginx

Result:

active (running)
Port 80
sudo ss -tulpn | grep :80

Result:

0.0.0.0:80
Local Application
curl http://localhost

The HTML application was returned successfully.


The overall AWS network.

10.0.0.0/16
Subnet

A smaller network inside the VPC.

Public:  10.0.1.0/24
Private: 10.0.2.0/24
Public Subnet

A subnet whose route table has a route to an Internet Gateway.

0.0.0.0/0 -> Internet Gateway
Private Subnet

A subnet without a direct Internet Gateway route.

Route Table

Controls where network traffic is sent.

Internet Gateway

Connects the VPC to the Internet.

Security Group

Controls allowed traffic to the EC2 instance.

EC2

The virtual server running Ubuntu.

Nginx

The web server serving the HTML application.

HTML

The application deployed on the EC2 instance.

Route Table vs Security Group
Route Table

Answers:

Where should the traffic go?

Example:

0.0.0.0/0 -> Internet Gateway
Security Group

Answers:

Is the traffic allowed to reach the EC2?

Example:

TCP 80 -> Allowed

Both must be configured correctly for the website to work.

