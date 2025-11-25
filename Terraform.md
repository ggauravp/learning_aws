# TERRAFORM
Terraform is an open-source Infrastructure as Code (IaC) tool developed by HashiCorp that allows users to define, provision, and manage cloud and on-premises infrastructure using a declarative configuration language, primarily HashiCorp Configuration Language (HCL) or JSON.lk<br>
It enables teams to automate the entire lifecycle of infrastructure, including creation, modification, and versioning, through human-readable configuration files that can be version controlled, reused, and shared.
- so basically terraform is tool that lets us create , manage , destroy the aws(cloud) infrastructure with the help of code called HCL or jSON can also be used , without interacting to aws console UI.
# How to Configure Terraform on Windows 10 WSL Ubuntu for AWS Provisioning
1. Enable WSL and Install Ubuntu
2. Update Ubuntu Packages
- Open the Ubuntu app and Run the following commands:
- `sudo apt update`
3. Install Terraform
- Download the Terraform package by running:
- `curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -`
- Add the HashiCorp Linux repository:
- `sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"`
- Update and install Terraform:
- `sudo apt update && sudo apt install terraform`
- Verify the installation:
- `terraform -version`
4. Download and install AWS CLI v2 by following the instructions
- `sudo apt update && sudo apt install unzip`
- `curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"`
- `unzip awscliv2.zip`
- `sudo ./aws/install`
- `aws --version`
- You should see version information printed out similar to this:
- `aws-cli/2.x.xx Python/3.x.xx Linux/4.x.xx botocore/2.x.xx`
5. Configure AWS CLI
- `aws configure`
6. Create a Terraform Configuration File
- `mkdir terraform-aws-demo && cd terraform-aws-demo`
7. Create a new file called main.tf
- `nano main.tf`
8. write the terraform code in HCL 
9. Initialize Terrform
- `terraform init`
10. Plan and Apply to Create Resources
- `terraform plan`
- `terraform apply`
11. verify the creation 
- Check your AWS console to verify whatever you have created(ec2 instance, s3 bucket,..) has been created successfully.

- Now That instance is created you can clone the project from github, create virtual environment, import requirements.txt and run the server and use the <instance-public-ip>:8000 to access the website from anywhere.<br>
- use following command to runserver so that the server runs in background also
- `nohup python manage.py runserver 0.0.0.0:8000 > server.log 2>&1 &`