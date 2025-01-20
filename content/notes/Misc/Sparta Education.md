![[Images/Pasted image 20241128112205.png|300]]

![[Images/Pasted image 20241128122456.png]]

# Pillars of SCRUM

![[Images/Pasted image 20241128114452.png]]

# Requirement Elicitation

![[Images/Pasted image 20241128122329.png|400]]

# User Story Structure

![[Images/Pasted image 20241128134023.png|600]]

Writing a good user story:
- Independent
- Negotiable
- Valuable
- Estimable
- Small
- Testable

# Acceptance Criteria

How we know when a user story is completed

## Structuring Acceptance Criteria

Break items down so they are small and testable

![[Images/Pasted image 20241128143347.png]]

## Happy, Sad and Alternative Scenarios

![[Images/Pasted image 20241128143746.png]]

## Estimation & Prioritisation

### Product Backlog

![[Images/Pasted image 20241129101433.png]]
### Story Points

![[Images/Pasted image 20241129101906.png]]

### Planning Poker

![[Images/Pasted image 20241129102520.png]]

### MoSCoW

![[Images/Pasted image 20241129103503.png]]

### MVP

![[Images/Pasted image 20241129103645.png]]

### Definitions of Done & Ready

![[Images/Pasted image 20241129104135.png]]
![[Images/Pasted image 20241129104205.png]]

![[Images/Pasted image 20241129104403.png]]

![[Images/Pasted image 20241129104442.png]]

![[Images/Pasted image 20241129104644.png]]

![[Images/Pasted image 20241129104813.png]]

# SCRUM Stages

![[Images/Pasted image 20241129105227.png]]

## Sprint Planning

![[Images/Pasted image 20241129105431.png]]

## Development

![[Images/Pasted image 20241129105449.png]]

## Daily SCRUM

![[Images/Pasted image 20241129105527.png]]

## Sprint Review

![[Images/Pasted image 20241129105606.png]]

## Sprint Retrospective

![[Images/Pasted image 20241129105723.png]]

![[Images/Pasted image 20241129110411.png]]

# Agile Manifesto

![[Images/Agile-Manifesto.png]]



# Interview Advice

Look at companies core values and work into response
- For example, if company has diversity as a core value
- "I love being able to work with people from different backgrounds, because I learn so much more from them"

If there is a general question e.g. what gets you up in the morning
- You can give a general answer
- But try to work job/interview into it
- "What gets me up in the morning to work as a software engineer, is how much I enjoy learning"

# Python Scripting

Why might Cloud Engineers choose Python over another language

# Azure

Creating a Resource Group called `cloudfun1`
- Creating a Virtual Network inside
	- Organise things into Subnets inside
		- `public-subnet`
			- Will contain VM that will run App
		- `private-subnet`
			- Will contain VM that will run DB

![[Images/Pasted image 20241210145118.png|300]]

Private SSH Key stays in `.ssh` folder, which is found at `C/Users/isaac/.ssh`

`ssh-keygen -t rsa -b 4096 -C "isaacklugman@gmail.com"` to generate ssh key
- 4096 is the length of the key in bytes

`.pub` is the public key, the one with no extension is the private key

## Creating a Virtual Network

>[!INFO]
>Azure Virtual Network (VNet) is the fundamental building block for your private network in Azure. VNet enables many types of Azure resources, such as Azure Virtual Machines (VM), to securely communicate with each other, the internet, and on-premises networks. VNet is similar to a traditional network that you'd operate in your own data center, but brings with it additional benefits of Azure's infrastructure such as scale, availability, and isolation.

Example naming convention for creating a cloud entity `cloudfun1-isaac-uks-test-vnet`

>[!INFO]
>Tags are name/value pairs that enable you to categorize resources

A VNet is for networking, you would deploy a VNet if you wanted to host a DB VM and an application VM for example - you would put them inside the same VNet so they can talk to each other

## VMs

In order to remote into our VMs, we upload our public SSH key to Azure

Go to the `SSH Keys` section Azure

When creating a new key, we can upload the public key generated on your personal machine

Example key name `cloudfun1-isaac-az-key`

When creating a VM we want to pick Use Existing Key stored in Azure

Example VM Net settings

![[Images/Pasted image 20241211123239.png]]


Once VM is created, you can go to Connect and choose Native SSH

# Understand what is the Cloud

## On-Premises vs. Cloud: Key Differences

To determine if something is in the cloud, consider these key differences from on-premises solutions:

1. Infrastructure location: Cloud services are hosted on remote servers, while on-premises solutions use local hardware.
2. Accessibility: Cloud resources are accessible via the internet, whereas on-premises systems typically require local network access.
3. Scalability: Cloud services offer easy scalability, while on-premises solutions have physical limitations.
4. Maintenance: Cloud providers handle maintenance, updates, and security, whereas on-premises systems require in-house management.
5. Cost model: Cloud services typically use a pay-as-you-go model, while on-premises solutions involve upfront hardware costs.

## Cloud Deployment Models

## Public Cloud

- Owned and operated by third-party providers
- Shared resources among multiple tenants
- Accessible over the internet
- Examples: AWS, Microsoft Azure, Google Cloud Platform

## Private Cloud

- Dedicated to a single organization
- Can be on-premises or hosted by a third party
- Offers greater control and customization
- Suitable for organizations with strict security requirements

## Hybrid Cloud

- Combines public and private cloud environments
- Allows data and applications to move between the two
- Offers flexibility and optimizes existing infrastructure
- Balances security and scalability needs

## Multi-Cloud

- Uses multiple cloud providers for different services
- Reduces vendor lock-in
- Optimizes performance and cost across providers
- Increases complexity in management

## Types of Cloud Services

## Infrastructure as a Service (IaaS)

- Provides virtualized computing resources over the internet
- Includes virtual machines, storage, and networking
- Users manage operating systems, storage, and deployed applications
- Examples: Amazon EC2, Microsoft Azure VMs

## Platform as a Service (PaaS)

- Offers a platform for developers to build, run, and manage applications
- Includes development tools, database management, and business analytics
- Abstracts the complexity of maintaining the underlying infrastructure
- Examples: Google App Engine, Heroku

## Software as a Service (SaaS)

- Delivers software applications over the internet
- Eliminates the need for installations and running applications on individual computers
- Provides automatic updates and patch management
- Examples: Salesforce, Google Workspace, Microsoft 365

## Advantages and Disadvantages of Cloud Computing

## Advantages

1. Cost-efficiency: Reduces upfront infrastructure costs
2. Scalability: Easily adjust resources based on demand
3. Flexibility: Access resources from anywhere with an internet connection
4. Automatic updates: Cloud providers manage software and security updates
5. Disaster recovery: Built-in data backup and recovery options

## Disadvantages

1. Internet dependency: Requires a stable internet connection
2. Security concerns: Data stored externally may be vulnerable to breaches
3. Limited control: Less control over underlying infrastructure
4. Potential downtime: Service interruptions can affect business operations
5. Compliance issues: May face challenges with data sovereignty and regulations

## OpEx vs. CapEx in Cloud Computing

Cloud computing shifts IT expenses from Capital Expenditure (CapEx) to Operational Expenditure (OpEx):

- CapEx: Large upfront investments in physical assets (e.g., servers, data centers)
- OpEx: Ongoing, pay-as-you-go expenses for cloud services

This shift allows businesses to reduce initial costs and align expenses with actual usage.

## Cloud Migration Cost Considerations

Migrating to the cloud is not always cheaper, especially in the short term. Factors to consider:

1. Migration costs: Data transfer, application refactoring, and training
2. Ongoing operational costs: Monthly service fees and potential bandwidth charges
3. Long-term savings: Reduced hardware maintenance and energy costs
4. Optimization: Proper resource management to avoid overspending

## Cloud Market Share

The cloud market is dominated by three major providers:

1. Amazon Web Services (AWS): 31% market share
2. Microsoft Azure: 25% market share
3. Google Cloud Platform (GCP): 11% market share

Other providers like Alibaba Cloud, Oracle Cloud, and IBM Cloud make up the remaining market share.

## Top 3 Cloud Providers: Key Strengths

## Amazon Web Services (AWS)

- Extensive service offerings
- Global infrastructure
- Strong enterprise adoption

## Microsoft Azure

- Seamless integration with Microsoft products
- Hybrid cloud capabilities
- Strong presence in enterprise markets

## Google Cloud Platform (GCP)

- Advanced data analytics and machine learning capabilities
- Competitive pricing
- Strong container and Kubernetes support

## Common Cloud Costs

When using cloud services, you typically pay for:

1. Compute resources (virtual machines, containers)
2. Storage (object storage, block storage, databases)
3. Network traffic (data transfer, load balancing)
4. Additional services (monitoring, security, AI/ML)

## The Four Pillars of DevOps and Cloud Connection

1. Collaboration: Cloud platforms facilitate teamwork and communication
2. Automation: Cloud services offer tools for automating deployment and scaling
3. Continuous Integration/Continuous Delivery (CI/CD): Cloud-native CI/CD pipelines streamline development
4. Monitoring: Cloud providers offer robust monitoring and logging solutions

These pillars are closely linked to cloud computing, as cloud platforms provide the tools and infrastructure to implement DevOps practices effectively.

# Linux Commands

- `uname -a` - Gives Linux version info
- `whoami` - Logged in username
- `cat /etc/shells` - Paths to the different shells on this Linux image
- `ps -p $$` - Shows the process of the shell your currently using
	- `ps -p` shows a given process id, `$$` represents the current shell process
- `history` - Shows the last 500 commands used
	- Use `!10` to execute the 10th command shown in `history`
	- `history -c` clears your history
- `curl` can be used to upload and download files, whereas `wget` is primarily for downloading files
- `file` - Get file info

`#!/bin/bash` is a shbang, tells you what shell to use to execute