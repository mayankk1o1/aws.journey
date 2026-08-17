# Jenkins Installation on AWS EC2 (Ubuntu)

In this project, I deployed and configured **Jenkins** on an **Ubuntu EC2 instance** hosted on AWS. Jenkins is an open-source automation server used to implement Continuous Integration and Continuous Deployment (CI/CD). This setup provides a cloud-based Jenkins server that can be used to automate software build, testing, and deployment workflows.

---

# Project Architecture

```
+-----------------------+
|   Local Windows PC    |
|  (PuTTY + Browser)    |
+----------+------------+
           |
           | SSH (Port 22)
           |
+----------v------------+
|    AWS EC2 Instance   |
|      Ubuntu Server    |
|-----------------------|
|  OpenJDK 21           |
|  Jenkins Service      |
|  Port 8080            |
+----------+------------+
           |
           | HTTP (Port 8080)
           |
+----------v------------+
|   Jenkins Dashboard   |
+-----------------------+
```

---

# 📌 Prerequisites

Before starting, I ensured the following were available:

- AWS Account
- Ubuntu EC2 Instance
- AWS Key Pair (.pem)
- PuTTY & PuTTYgen (Windows)

---

# Step 1: Launch an Ubuntu EC2 Instance

### Actions Performed

- Logged into the AWS Management Console.
- Navigated to **EC2 Dashboard**.
- Launched a new **Ubuntu Server** instance.
- Created and downloaded an AWS Key Pair.
- Launched the instance.

### Security Group Configuration

| Rule | Port | Purpose |
|------|------|---------|
| SSH | 22 | Remote Login |
| Custom TCP | 8080 | Jenkins Dashboard |

### Outcome

An Ubuntu EC2 instance was successfully created with public internet access.

---

# Step 2: Connect to the EC2 Instance

Since I was using Windows, I connected to the server using **PuTTY**.

### Actions Performed

- Converted the `.pem` key into a `.ppk` file using **PuTTYgen**.
- Opened PuTTY.
- Connected using:

```text
Host Name : ubuntu@<EC2_Public_IP>
Port      : 22
```

- Selected the `.ppk` key under:

```
Connection
    └── SSH
          └── Auth
```

### Outcome

Successfully connected to the Ubuntu server through SSH.

---

# Step 3: Update the Ubuntu Server

Updated the package repository and installed the latest updates.

```bash
sudo apt update
sudo apt upgrade -y
```

### Why?
- Good Practice
- Updates package information.
- Installs security patches.
- Ensures package compatibility.

### Outcome

Ubuntu server updated successfully.

---

# Step 4: Install Java

Jenkins requires Java to run.

### Install OpenJDK

```bash
sudo apt install fontconfig openjdk-21-jre -y
```

### Verify Installation

```bash
java -version
```

### Outcome

Java was installed successfully and verified.

---

# Step 5: Install Jenkins

- Install thru Jenkin Linux download page and download any version ( I used the weekly release)

### Outcome

Jenkins was successfully installed on the Ubuntu server.

---

# Step 6: Start Jenkins Service

### Start Jenkins

```bash
sudo systemctl start jenkins
```

### Enable Jenkins on Boot

```bash
sudo systemctl enable jenkins
```

### Check Status

```bash
sudo systemctl status jenkins
```

Expected Output

```
Active: active (running)
```

### Outcome

Jenkins service started successfully and was configured to start automatically after every reboot.

---

# Step 7: Configure AWS Security Group

Added an inbound rule for Jenkins.

| Type | Protocol | Port | Source |
|------|----------|------|--------|
| Custom TCP | TCP | 8080 | My IP (Recommended) | or 0.0.0.0/0 (For testing)

### Why?

This allows external access to the Jenkins web interface.

### Outcome

Jenkins became accessible through a web browser.

---

# Step 8: Access Jenkins

Opened a browser and visited:

```text
http://<EC2_Public_IP>:8080
```

Retrieved the initial administrator password:

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Entered the password on the Jenkins setup page.

Installed the **Suggested Plugins** and created an administrator account.

### Outcome

Successfully logged into the Jenkins Dashboard.

---

# Final Result

Successfully deployed a Jenkins server on an Ubuntu EC2 instance hosted on AWS.

The Jenkins instance is now:

- Running as a Linux service
- Accessible through the browser
- Ready to integrate with GitHub, Docker, and Kubernetes

---

# 🛠️ Technologies Used

- Amazon Web Services (AWS)
- EC2
- Ubuntu Linux
- Jenkins
- OpenJDK 21
- PuTTY
- PuTTYgen
- SSH
- Linux Terminal

---

# 📚 Commands Used

## Start Jenkins

```bash
sudo systemctl start jenkins
sudo systemctl enable jenkins
```

## Check Jenkins Status

```bash
sudo systemctl status jenkins
```

## Retrieve Initial Password

---

# Key Learnings

- Learned how to provision a cloud-based Ubuntu server using AWS EC2.
- Connected securely to a remote Linux server using SSH and key-based authentication.
- Installed Java as a prerequisite for Jenkins.
- Configured the official Jenkins repository.
- Installed and managed Jenkins using Linux system services.
- Configured AWS Security Groups to expose Jenkins on port 8080.
- Accessed and initialized Jenkins through its web interface.
- Built the foundation for implementing CI/CD pipelines on AWS.

---




