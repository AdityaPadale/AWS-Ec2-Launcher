# Launching an EC2 Instance on AWS 🚀  

This guide explains how to launch an **Amazon EC2 instance** using both the **AWS Management Console** and the **AWS CLI**.  

---

## ✅ Prerequisites
- AWS account → [Sign up here](https://aws.amazon.com/)  
- IAM user with EC2 permissions  
- AWS CLI installed → [Install Guide](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)  
- Configured AWS CLI → `aws configure`  
- Key pair for SSH access  

---

# 🌐 Method 1: Using AWS Management Console  

### 1. Log in to AWS Console  
Go to [AWS Console](https://aws.amazon.com/console/) and sign in.  
![AWS Console](https://d1.awsstatic.com/console/console-homepage.png)  

---

### 2. Open EC2 Service  
Search **EC2** in the search bar and open it.  
![EC2 Dashboard](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/images/EC2Dashboard.png)  

---

### 3. Click **Launch Instance**  
From the EC2 dashboard, select **Launch Instance**.  
![Launch Instance](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/images/launch-instance-button.png)  

---

### 4. Choose an Amazon Machine Image (AMI)  
Pick your OS (Amazon Linux 2, Ubuntu, etc.).  
![Choose AMI](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/images/choose-ami.png)  

---

### 5. Select Instance Type  
Choose instance type (e.g., `t2.micro` for free tier).  
![Instance Type](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/images/choose-instance-type.png)  

---

### 6. Create / Select Key Pair  
Download a **.pem** key file for SSH access.  
![Key Pair](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/images/key-pair.png)  

---

### 7. Configure Security Group  
Allow **SSH (22)**, **HTTP (80)**, or other required ports.  
![Security Group](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/images/security-group.png)  

---

### 8. Launch the Instance  
Click **Launch Instance** and wait until status = **Running**.  
![Running Instance](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/images/running-instance.png)  

---

### 9. Connect to Instance  
- Select your instance → **Connect**  
- Use SSH command:  
```bash
ssh -i your-key.pem ec2-user@<Public-IP>
