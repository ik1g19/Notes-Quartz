# Concepts

#docker #django #aws #infrastructure-as-code #cicd 

---
# Summary

![](https://www.youtube.com/watch?v=o22qYKDCGbU)

[GitHub Repo](https://github.com/ik1g19/django-aws-ecs-terraform)

1. **Create an EC2 Ubuntu instance**
    - This step involves launching a virtual server (EC2 instance) running Ubuntu on AWS. This server will be used for various tasks such as setting up a self-hosted runner and performing initial configurations. EC2 stands for **Elastic Compute Cloud**. It is a service provided by Amazon Web Services (AWS) that allows users to rent virtual servers (instances) to run their applications
2. **Install Packages on EC2 Instance (Docker, AWS CLI)**
    - After the EC2 instance is up and running, you will install necessary software packages. Docker is required for containerizing your application, and AWS CLI is needed for interacting with AWS services programmatically.
3. **Configure AWS CLI on EC2, Also on the Local Machine**
    - AWS CLI configuration involves setting up access credentials on both the EC2 instance and your local machine. This allows you to manage AWS services from both environments, ensuring smooth deployment and management processes.
4. **Setup Self Hosted runner on EC2**
    - A self-hosted runner is a server that runs your GitHub Actions workflows. Setting up a self-hosted runner on the EC2 instance allows you to execute your CI/CD pipeline directly on this instance, providing more control and potentially reducing costs.
5. **Create DB Password on AWS Secret Manager**
    - AWS Secrets Manager is used to securely store sensitive information such as database passwords. In this step, you will create a secret to store your database password, which your application can retrieve securely during deployment.
6. **Create ECR Repository on AWS**
    - Amazon Elastic Container Registry (ECR) is a fully managed container registry. You'll create a repository here to store your Docker images, which will be used to deploy your Django application on ECS Fargate.
7. **Create CI/CD Pipeline using GitHub Actions**
    - This step involves setting up a continuous integration and continuous deployment (CI/CD) pipeline using GitHub Actions. The pipeline automates the process of building, testing, and deploying your application whenever you push changes to your GitHub repository.
8. **GitHub Actions (Build)**
    - In this part of the pipeline, you'll configure GitHub Actions to build your Django application. This includes steps such as installing dependencies, running tests, and creating Docker images of your application.
9. **Create Infrastructure using Terraform**
    - Terraform is an Infrastructure as Code (IaC) tool that allows you to define and provision your AWS infrastructure using code. In this step, you will write Terraform scripts to create and manage the necessary AWS resources for your Django application.
10. **GitHub Actions (Build and Deploy)**
    - This step extends the GitHub Actions pipeline to include deployment. After building the application, the pipeline will push the Docker image to ECR and then deploy the application to ECS Fargate, using the infrastructure defined by Terraform.
11. **Add SSL and domain**

# Explanation of Project Structure

![[Pasted image 20240530155029.png|200]]

- `.github/workflows/aws-ecs.yml`
    - **Purpose**: Contains the GitHub Actions workflow configuration. This file defines the steps to automate the deployment process to AWS ECS Fargate whenever changes are pushed to the repository.
- `django/`
    - **Purpose**: Contains the Django application and related files.
    - `backend/`: The core Django application directory where your Django apps reside.
	    - `__init__.py`
		    - **Purpose**: Marks the directory as a Python package. It can be an empty file.
		- `admin.py`
		    - **Purpose**: Registers Django models to the admin interface, allowing you to manage them through the Django admin panel.
		- `asgi.py`
		    - **Purpose**: Entry point for ASGI-compatible web servers to serve your project. ASGI (Asynchronous Server Gateway Interface) is a standard for Python asynchronous web apps and servers to communicate.
		- `settings.py`
		    - **Purpose**: Contains all the settings and configuration for your Django project, such as database settings, installed apps, middleware, templates configuration, etc.
		- `urls.py`
		    - **Purpose**: Defines the URL patterns for your project. It maps URL paths to views.
		- `wsgi.py`
		    - **Purpose**: Entry point for WSGI-compatible web servers to serve your project. WSGI (Web Server Gateway Interface) is a standard for Python web app servers to communicate with applications.
    - `build-process/`: Contains configuration and scripts for building the Docker image.
        - `docker-backend-django/`:
            - `config/`: Contains configuration files for the Docker build.
            - `scripts/`: Contains scripts related to the Docker build process.
            - `Dockerfile`: Defines the instructions for building the Docker image for the Django application.
            - `docker-compose-django-backend.yml`: A Docker Compose file for local development, possibly to run multiple services like Django, PostgreSQL, etc.
            - `local.backend.env`: Environment variables for local development.
    - `requirements/`: Contains the Python dependencies required by the Django application.
    - `manage.py`: Django's command-line utility for administrative tasks.
- `terraform/`
    - **Purpose**: Contains Terraform configurations for provisioning infrastructure on AWS.
    - `.terraform/`: Internal directory created by Terraform to store plugin binaries and state-related files.
    - `modules/`: Typically contains reusable Terraform modules, though it's empty here.
    - `terraform.tfstate.d/`: Directory for Terraform state files, which track the state of the infrastructure managed by Terraform.
    - `terraform.lock.hcl`: Lock file ensuring consistent provider versions.
    - `main.tf`: The main configuration file where the AWS resources are defined.
    - `outputs.tf`: Defines the outputs of your Terraform configuration, such as DNS names, IDs, etc.
    - `provider.tf`: Specifies the provider (AWS in this case) and configuration settings.
    - `variables.tf`: Defines the input variables for the Terraform configuration.


# Create an EC2 Ubuntu Instance

An EC2 instance is a virtual server that runs in the AWS cloud

Go to the EC2 dashboard on AWS console and select **Launch Instance**

You will be prompted to select an Amazon Machine Image (AMI)

An AMI is a pre-configured virtual machine image that includes the operating system, application server, and other software needed to run your application

- Name the instance
- Pick an application instance - we are using Ubuntu
- You can then select an instance type, which will affect the power of the vm
- Create a new key-pair, once you do download the file, this will be used to ssh into your instance later
	- It should download a .pem file when you click create pair
- Under network settings, allow HTTPS and HTTP traffic from the internet
- Then configure the storage volumes you want to use
- Select **Launch Instance**

# Install Packages on EC2 Instance (Docker, AWS CLI)

Go to the location of your downloaded .pem file

On the AWS Instances panel, select your instance and then select connect

This will bring up a screen which has a command ready that you can copy and paste to ssh into the instance

```sh
ssh -i "git.pem" ubuntu@ec2-13-53-151-193.eu-north-1.compute.amazonaws.com
```

First we update since it is a fresh machine

```sh
sudo apt-get update
```

Then we install docker

```sh
sudo apt install docker.io -y
```

Then we add the user `ubuntu` to the `docker` group

```sh
sudo usermod -aG docker ubuntu
```

By adding the `ubuntu` user to the `docker` group, you grant this user the ability to run Docker commands without needing to use `sudo` every time

Then run

```sh
newgrp docker
```

to change the current users group id to `docker`

Then we run 

```sh
sudo chmod 777 /var/run/docker.sock
```

This changes the permissions of the Docker socket file (`/var/run/docker.sock`) to make it readable, writable, and executable by all users

## Install AWS CLI

Next we have to install the cli for aws

We download the installer

```sh
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
```

Install `unzip`

```sh
sudo apt-get install unzip -y
```

Unzip the installer

```sh
unzip awscliv2.zip
```

And install it

```sh
sudo ./aws/install
```

# Configure AWS CLI on EC2

Next we have to create a secret key and access key

Search **IAM** on the AWS console

Go to `Users` and click **Create user**

Click Next and then on Permissions Options select **Attach Policies Directly**

Select `AdministratorAccess` from the list of policies and select Next, then Create user

Once the user has been created, select the user from the list and then select the **Security Credentials** tab

Select **Create Access Key**

Select the Use case as CLI

Provide a description for the access key and click Create, you can then download the access keys

Go back to the EC2 instance terminal and write

```sh
aws configure
```

It will ask for your access key, this is your first key

The secret access key is your second

When it asks for the Default region name, enter the same region that your instance was created on

# Setup Self Hosted runner on EC2

Go to the repository you want to setup a runner for

Go to the Settings tab and Select **Actions** and then **Runners**, then **New Self Hosted Runner**

Select the runner image to be used, in this example we have been using linux

Copy the download and configure commands to setup the GitHub actions runner

```sh
# Create a folder
$ mkdir actions-runner && cd actions-runner 
# Download the latest runner package   
$ curl -o actions-runner-linux-x64-2.316.1.tar.gz -L https://github.com/actions/runner/releases/download/v2.316.1/actions-runner-linux-x64-2.316.1.tar.gz
# Extract the installer   
$ tar xzf ./actions-runner-linux-x64-2.316.1.tar.gz
```

```sh
# Create the runner and start the configuration experience
./config.sh --url https://github.com/ik1g19/django-aws-ecs-terraform --token ATONFA23GGD3QR5TTVBYRIDGKSYSI
```

During configuration leave all the values default

The next step is to create a system service to start the GitHub runner whenever the Instance is started

```sh
sudo nano /etc/systemd/system/run-script.service
```

```
[Unit]  
Description=Script Runner Service  
After=network.target

[Service]  
Type=simple  
Restart=always  
User=ubuntu  
WorkingDirectory=/home/ubuntu/actions-runner  
ExecStart=/home/ubuntu/actions-runner/run.sh

[Install]  
WantedBy=multi-user.target
```

We now have to reload the daemon so we can enable the service

```sh
sudo systemctl daemon-reload   
sudo systemctl enable run-script
```

Then, to start the service

```sh
sudo systemctl start run-script
```

# Create DB Password on AWS Secret Manager

```sh
aws ssm put-parameter --name "/dev/djangoapi/db/password" --value "admin123" --type String --tags '[{"Key":"Region","Value":"eu-north-1"},{"Key":"Environment", "Value":"Dev"},{"Key":"Service", "Value":"admin123"}]'
```

This command is used to store a database password in AWS Systems Manager Parameter Store. By doing this, you can securely manage and retrieve sensitive configuration data such as passwords without hardcoding them in your application code. The tags provide additional metadata that can help with organization, access control, and cost allocation.

| **Command Part**                                                                                                              | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| ----------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `aws ssm put-parameter`                                                                                                       | This is the base command to add a parameter to the AWS Systems Manager Parameter Store.                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `--name "/dev/djangoapi/db/password"`                                                                                         | This specifies the name of the parameter. In this case, the parameter is named "/dev/djangoapi/db/password", which suggests it is a password for a database used by a Django API in the development environment.                                                                                                                                                                                                                                                                                                                  |
| `--value "admin123"`                                                                                                          | This sets the value of the parameter. Here, the value being stored is "admin123".                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `--type String`                                                                                                               | This specifies the type of the parameter. The type "String" indicates that the value is a plain text string. Other possible types include "StringList" and "SecureString".                                                                                                                                                                                                                                                                                                                                                        |
| `--tags '[{"Key":"Region","Value":"eu-north-1"},{"Key":"Environment", "Value":"Dev"},{"Key":"Service", "Value":"admin123"}]'` | This adds tags to the parameter. Tags are key-value pairs that can help you organize and manage your AWS resources. The tags added in this command are: <ul><li>**Region: eu-north-1**: Indicates the AWS region.</li><li>**Environment: Dev**: Indicates the environment (development in this case).</li><li>**Service: admin123**: Indicates a service-related tag, although in this case, it seems to duplicate the password value, which might be a mistake or intentional based on some internal tagging strategy.</li></ul> |

# Create ECR Repository on AWS

Now we want to be able to push our docker images to ECR

Go to the AWS console and search Elastic Container Registry (or ECR)

Click **Create**

Name the repository and click Create Repository

Now the repo has been created, copy the URI in the table next to its name

Open the `main.tf` terraform file in your repository

Replace the `app_image` field with the URI from ECR

# Create CI/CD Pipeline using GitHub Actions

In the GitHub workflow file `aws-ecs.yml` we want to update the `AWS_REGION` to the correct region

Comment out the deploy section in the GitHub workflow, since the infrastructure is not ready yet we don't want to run the deployment

Go to the settings tabs of your GitHub repository, go to **Secrets and variables** and then **Actions**

Go to **Repository Secrets** and create `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`

Enter the secret keys that you downloaded from AWS in [[#Configure AWS CLI on EC2]]

You can now push the code from your GitHub repository, you will see the building on GitHub Actions, and you will see the completed image on ECR when it is finished

# Create Infrastructure using Terraform

You now need to install AWS CLI on your development machine and run `aws configure` for the initial setup, where you will need to input your access key and secret key

Make sure terraform is installed as well using Chcolatey

```
choco install terraform
```

Navigate to the project terraform directory and run

```
terraform workspace new eu-north-1
```

and

```
terraform workspace select eu-north-1
```

and then

```
terraform init
```

Running `terraform plan` will list the changes that terraform is going to make to your AWS account

Run

```
terraform apply
```

To apply the terraform plan, this will take 10 minutes

We can now uncomment the deployment code in our GitHub actions workflow

Once the project has been built and deployed, you need to go to ECS to get the public URI so that you can access your Django application

We need to copy the right endpoint for the AWS Database, so we search **RDS** on AWS and go to **Databases**, then we copy the endpoint

So we go to the **Django** application folder in our GitHub repository, then **backend**, and then `settings.py`

Under `DATABASES`, we then update the `HOST` field so that it points to the right endpoint

You then need to deploy and rebuild the project again

