# Terraform-work

### Introduction
Terraform is a popular Infrastructure as Code (IaC) tool developed by HashiCorp, and it’s widely used for provisioning, managing, and automating infrastructure across various cloud providers
(e.g., AWS, Azure, Google Cloud) and on-premises environments.


## Installation  (Linux)

### 1. Update the System:
```
sudo apt update && sudo apt upgrade -y
```

### 2. Install Dependencies:
```
sudo apt install -y gnupg software-properties-common curl
```

### 3. Add the HashiCorp GPG Key:
```
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
```

### 4. Add the HashiCorp Repository:
```
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
```

### 5. Install Terraform:
```
sudo apt update
sudo apt install terraform -y
```
-> Verify Terraform
```
terraform -version
```
![image](https://github.com/user-attachments/assets/6ec3007e-8693-4f3c-a969-1c572517946c)


------------------------------------------------------------------------------------------------------
## AWS CLI installation 
```
sudo snap install aws-cli --classic
```
![image](https://github.com/user-attachments/assets/decca2a0-519e-4415-a402-a88ba48325f7)

-------------------------------------------------------------------------------------------------------

## AWS setup

### 1. IAM (Identify and Access management)
**-> Go to user groups in IAM -> Create a User Group
![image](https://github.com/user-attachments/assets/db28da02-5622-48e8-ba56-172f99c005fb)


==Give it Above permissions==

**-> Create User

![image](https://github.com/user-attachments/assets/f974268e-67b4-4d16-81e3-76bcf22c9ccf)


**-> Attach it with user Group of step 1

![image](https://github.com/user-attachments/assets/c15d734d-ee96-484e-a545-9a42f6c53f57)


**-> Create Access key

**-> Select AWS CLI

![image](https://github.com/user-attachments/assets/2b89441d-eac9-4e42-a468-aba663eb5440)


**-> so access key has been created now use this in AWS CLI
![image](https://github.com/user-attachments/assets/a4dead33-2a33-4c3d-841d-9af37f3322ab)


-----------------------------------------------------------------------------------------------------------------------
## Configure AWS:
```
aws configure
```
-> Manually Adding AWS Credentials
-
```
aws_access_key_id = YOUR_ACCESS_KEY
aws_secret_access_key = YOUR_SECRET_KEY
region = ap-south-1
```
-> Writing the Terraform Configuration File
-
```
mkdir terraform-ec2 && cd terraform-ec2
```
-> let's create a EC2 instance through code: - 
Create a file named ***main.tf***, and add the following configuration:

``` for example
provider "aws" {
  profile = "default"
  region  = "eu-north-1"
}

resource "aws_instance" "UGO_Server" {
  ami           = "ami-09a9858973b288bdd"
  instance_type = "t3.micro"
  subnet_id     = "subnet-052ed4bb67ed2eecf"
  
  tags = {
    Name = "MyNCAAInstance"
  }
}

```
use command 
```
nano main.tf
```
![image](https://github.com/user-attachments/assets/7b0c5e33-6727-423a-b6d9-62baffb8e6ab)



## Initializing and Applying Terraform

we need to initialize Terraform first !!
```
terraform init
```
![image](https://github.com/user-attachments/assets/fecf7b6d-bc14-4389-8bd8-b3abfda56100)



-> Check the Execution Plan
by Running
```
terraform plan
```
![image](https://github.com/user-attachments/assets/72674105-12f9-4de5-90ee-de31c20874ff)



-> Deploy your EC2 instance:
```
terraform apply -auto-approve
```
![image](https://github.com/user-attachments/assets/29418a12-4dc7-46f4-a533-d9d5f59359bd)


### In AWS console
-> Instance has been created !!

![image](https://github.com/user-attachments/assets/aae40bc8-4894-404e-82bc-1f63f6e80cd7)


-> Now Destroying the Infrastructure
```
terraform destroy -auto-approve
```
![image](https://github.com/user-attachments/assets/f7658b5a-d307-4f2b-b71d-92ada189905b)


-> In AWS

![image](https://github.com/user-attachments/assets/77ee7f45-5ffb-4626-9f31-ae8e4e8e2db7)







