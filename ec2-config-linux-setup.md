EC2 Instance Basic Setup (Ubuntu)

1. Connect to EC2

        ssh -i your-key.pem ubuntu@your-ec2-public-ip

2. Update System Packages

        sudo apt-get update
        sudo apt-get upgrade -y
    
3. Install Required Utilities

        sudo apt-get install -y unzip curl
    
AWS CLI Installation

4. Download AWS CLI

        curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
    
5. Extract the Installer

        unzip awscliv2.zip
    
6. Install AWS CLI

        sudo ./aws/install
    
7. Verify Installation

        aws --version
    
AWS CLI Configuration

8. Configure AWS CLI

        aws configure

Provide:
    
        AWS Access Key ID
        AWS Secret Access Key
        Default region (e.g., ap-south-1)
        Default output format (json)
