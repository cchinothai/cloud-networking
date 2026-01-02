
# Build a Virtual Private Cloud

**Author:** Cody Chinothai  
**Email:** cchinothai@gmail.com

---

## Build a Virtual Private Cloud (VPC)

![Image](http://learn.nextwork.org/enthusiastic_turquoise_radiant_monstera_deliciosa/uploads/aws-networks-vpc_2facf927)

---

## Introducing Today's Project!

Goal: Create an Amazon VPC and configure it with a public subnet and internet gateway

### What is Amazon VPC?

Amazon VPC is a fundamental part of setting up network traffic for your resources in AWS, such as your EC2 compute instance. Setting this up with an internet gateway is how you make your resources publicly accessible to outside traffic. 

We setup a VPC in AWS and configured subnets / internet gateways through the console and via the AWS CLI 

### Personal reflection

// Project time NA

One thing I didn't expect was the ease of creating such resources with either method.  You do have to be careful not to assign new subnets to your default VPC or potentially creating overlapping CIDR ranges with existing VPCs

---

## Virtual Private Clouds (VPCs)

### What I did in this step

In this step, we will access the VPC console in AWS to create our virtual private cloud. 

### How VPCs work

Virtual Private Clouds are your own delegated space within the cloud where you can control network traffic and public/private access to your resources. VPCs are setup with a specific CIDR range of allowable IP addresses.

We can distribute our vpc into different subnets that allow us to group resources. 

### Why there is a default VPC in AWS accounts

There is a default VPC in a standard AWS account because it is requirement for resources like EC2 compute in order to run properly. While some services can run without a VPC, there are many that need an isolated network setup. 

![Image](http://learn.nextwork.org/enthusiastic_turquoise_radiant_monstera_deliciosa/uploads/aws-networks-vpc_2facf927)

### Defining IPv4 CIDR blocks

To set up my VPC, I had to define an IPv4 CIDR block, which is an assigned block of IP addresses within our network. since we chose the CIDR block 10.0.0.0/16, we are allowed 16 varying bits (the last 2 IPV4 digits) which give us 2^16 possible IP addresses. 

---

## Subnets

### What I did in this step

Now, let's configure a subnet within the VPC we created

### Creating and configuring subnets

Subnets are smaller individual sections within your VPC network. There are already subnets existing in my account, one for every availability zone. 

### Public vs private subnets

A private subnet is meant to not have internet access so that it can uphold resources that you don't want publicly accessible. 

Our subnet is not considered public yet because we have yet to initialize an internet gateway that allows public access. 

![Image](http://learn.nextwork.org/enthusiastic_turquoise_radiant_monstera_deliciosa/uploads/aws-networks-vpc_157c4219)

### Auto-assigning public IPv4 addresses

We enable auto-assign public IPv4 addresses because by default, created resources are only given private IP addresses at the time of creation. 

Enabling this option assigns a public IP address for any EC2 instance created within your subnet. 

---

## Internet gateways

### What I did in this step

Next, let's connect an internet gateway to make our subnets public. 

### Setting up internet gateways

Internet gateways are connections that bridge your VPC traffic to the global internet. This enables applications to be discoverable and accessible to users outside of your private network. 

Attaching an internet gateway to a VPC means that the resources in your private network are now connected to the internet, and network traffic can flow between the two in both directions via the internet gateway. 

** note: you will have to configure the internet gateway connection in the subnet's route table.

![Image](http://learn.nextwork.org/enthusiastic_turquoise_radiant_monstera_deliciosa/uploads/aws-networks-vpc_4ae90410)

---

## Using the AWS CLI

### What I'm doing in this extension

We can also configure a VPC using the AWS CLI 

### Exploring CloudShell and CLI

### Debugging my setup

To set up a VPC or a subnet, you can use the command: 
- aws ec2 create-subnet --vpc-id [vpc-id]


Make sure to avoid errors by: 
- checking that the CIDR specifies the start of the range (ex. 10.0.0.0/24 instead of 10.0.0.1/24)
- checking that you do not have overlapping ranges with other subnets in the same VPC ). 


![Image](http://learn.nextwork.org/enthusiastic_turquoise_radiant_monstera_deliciosa/uploads/aws-networks-vpc_9b2465411)

### Comparing CloudShell vs AWS Console

Setting up VPC resources in CloudShell can be more intuitive rather than using the UI given that can take precautions in identifying existing resources in your VPC by listing them out and creating the relevant subnet / igw resources given you have the vpc id. 

---

---
