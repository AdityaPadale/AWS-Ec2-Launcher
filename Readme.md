#!/bin/bash

# --- Configuration Variables ---
# You can change these values

KEY_NAME="my-cli-key"
SECURITY_GROUP_NAME="my-cli-sg"
INSTANCE_TYPE="t2.micro"
# Get the latest Amazon Linux 2 AMI ID for the us-east-1 region
# To find an AMI for a different region, use the AWS Console or EC2 API.
AMI_ID="ami-0c55b159cbfafe1f0" 

echo "🚀 Starting EC2 instance launch..."

# 1. Create a new key pair and save the private key to a .pem file
echo "🔑 Creating key pair: $KEY_NAME"
aws ec2 create-key-pair --key-name "$KEY_NAME" --query 'KeyMaterial' --output text > "$KEY_NAME.pem"
# Secure the key file
chmod 400 "$KEY_NAME.pem"

# 2. Get the default VPC ID
VPC_ID=$(aws ec2 describe-vpcs --filters "Name=isDefault,Values=true" --query "Vpcs[0].VpcId" --output text)
echo "🌐 Using default VPC: $VPC_ID"

# 3. Create a security group to allow SSH access
echo "🔒 Creating security group: $SECURITY_GROUP_NAME"
GROUP_ID=$(aws ec2 create-security-group --group-name "$SECURITY_GROUP_NAME" --description "Allow SSH access" --vpc-id "$VPC_ID" --query 'GroupId' --output text)

# 4. Add a rule to the security group to allow inbound SSH traffic (port 22)
aws ec2 authorize-security-group-ingress --group-id "$GROUP_ID" --protocol tcp --port 22 --cidr 0.0.0.0/0

echo " firewall rule for SSH..."

# 5. Launch the EC2 instance with the created resources
echo "💻 Launching instance of type $INSTANCE_TYPE with AMI $AMI_ID..."
INSTANCE_ID=$(aws ec2 run-instances \
    --image-id "$AMI_ID" \
    --instance-type "$INSTANCE_TYPE" \
    --key-name "$KEY_NAME" \
    --security-group-ids "$GROUP_ID" \
    --query 'Instances[0].InstanceId' \
    --output text)

echo "✅ Instance launch initiated! Instance ID: $INSTANCE_ID"
echo "⏳ Waiting for instance to enter 'running' state..."

aws ec2 wait instance-running --instance-ids "$INSTANCE_ID"

PUBLIC_IP=$(aws ec2 describe-instances --instance-ids "$INSTANCE_ID" --query 'Reservations[0].Instances[0].PublicIpAddress' --output text)

echo "🎉 Instance is running! Connect using:"
echo "ssh -i \"$KEY_NAME.pem\" ec2-user@$PUBLIC_IP"
