# Terraform--creating-instance

Terraform
---------
Infrastructure Management Tool.


We need to write script for 
1. Connecting to aws environment (providers)
2. Launch instance (resources)

Install terraform in machine and set the path in environment variables.

Terraform Commands
------------------
terraform init     --> initialize plugins
terraform plan     --> checks all resources provided or not
terraform apply -auto-approve    --> starts creating resources
terraform destroy  --> deletes the resources


Terraform Credentials
----------------------

Access key ID- AKIAS5QJFNKWB2YIVC22

Secret access key - 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

provider.tf
-----------
provider "aws" {
  region     = "us-east-1"
  access_key = "AKIAS5QJFNKWB2YIVC22"
  secret_key = "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"
  version = "~> 4.0"
}


aws-instance.tf
---------------
resource "aws_instance" "web" {
  ami           = "ami-090fa75af13c156b4"
  instance_type = "t2.micro"
  key_name   = "8ambatch"

  tags = {
    Name = "Terraform"
  }
}

aws_security_group.tf
---------------------
resource "aws_security_group" "ssh_port" {
  name        = "allow_ssh"
  description = "SSH port"

  ingress {
    description      = "SSH"
    from_port        = 22
    to_port          = 22
    protocol         = "tcp"
    cidr_blocks 	 = ["0.0.0.0/0"]
  }

  egress {
    from_port        = 0
    to_port          = 0
    protocol         = "-1"
    cidr_blocks      = ["0.0.0.0/0"]
  }

  tags = {
    Name = "ssh_security_group"
  }
}




open SSH portnumber 22 in security group and try to connect to ec2 instance. we will be able to connect. 

/c/Linux AWS DevOps/Terraform/8ambatch

terraform init
terraform plan
terraform apply (instance is created)
terraform destroy









