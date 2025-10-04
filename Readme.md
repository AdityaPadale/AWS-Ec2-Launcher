# Launching an EC2 Instance on AWS 

This guide explains how to launch an **Amazon EC2 instance** using both the **AWS Management Console** and the **CLI**.  

---

## Prerequisites
- AWS account → [Sign up here](https://aws.amazon.com/)  
- IAM user with EC2 permissions  
- Git bash should be installed and setup

---

# Method 1: Using AWS Management Console  

### 1. Log in to AWS Console  
Go to [AWS Console](https://aws.amazon.com/console/) and sign in.  

---

### 2. Open EC2 Service  
Search **EC2** in the search bar and open it.  

---

### 3. Click **Launch Instance**  
From the EC2 dashboard, select **Launch Instance**.  

---

### 4. Choose an Amazon Machine Image (AMI)  
Pick your OS (Amazon Linux 2, Ubuntu, etc.).  

---

### 5. Select Instance Type  
Choose instance type (e.g., `t2.micro` for free tier).  

---

### 6. Create / Select Key Pair  
Download a **.pem** key file for SSH access.  

---

### 7. Configure Security Group  
Allow **SSH (22)**, **HTTP (80)**, or other required ports.  

---

### 8. Launch the Instance  
Click **Launch Instance** and wait until status = **Running**.  

---

### 9. Connect to Instance  
- Select your instance → **Connect**  
- Use SSH command: Git ash 
```bash
ssh -i your-key.pem ec2-user@<Public-IP>
