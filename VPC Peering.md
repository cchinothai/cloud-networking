<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Peering

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-peering)

**Author:** Cody Chinothai  
**Email:** cchinothai@gmail.com

---

## VPC Peering

![Image](http://learn.nextwork.org/enthusiastic_turquoise_radiant_monstera_deliciosa/uploads/aws-networks-peering_88727bef)

---

## Introducing Today's Project!

### What is Amazon VPC?

-------------

### How I used Amazon VPC in this project

---------------------

### One thing I didn't expect in this project was...

----------------------

### This project took me...

-------------------

---

## In the first part of my project...

### Step 1 - Set up my VPC

In this step, we'll recreate VPCs from scratch using the VPC resource map. 

### Step 2 - Create a Peering Connection

In this step, I will setup a VPC peering connection to link our VPCs. This will route traffic between them using private IP addresses. 

### Step 3 - Update Route Tables

Now with our peering connection set up, we will update our route tables to define traffic flow between VPC 1 and VPC 2. 

### Step 4 - Launch EC2 Instances

Now, lets launch EC2 instances to setup our connectivity tests between our VPCs. 

---

## Multi-VPC Architecture

I started my project by launching my VPC setup through the resource map creation. We created 2 VPCs each with 1 public subnet but different CIDR blocks so we don't have overlapping traffic when connected. 

The CIDR blocks for VPCs 1 and 2 are 10.1.0.0/16 and 10.2.0.0/16 respectfully to prevent routing conflicts and connectivity issues. 

### I also launched 2 EC2 instances

Note: we chose not to setup key pairs in this case since we will only be connecting through EC2 instance connect. This auto creates/manages key pairs for us. 

![Image](http://learn.nextwork.org/enthusiastic_turquoise_radiant_monstera_deliciosa/uploads/aws-networks-peering_11111111)

---

## VPC Peering

A VPC peering connection is routes traffic between 2 VPCs using their private IP addresses. One VPC will act as the requestor and initiate the connection. The other VPC will be the accepter to either allow or deny the connection. 

VPCs would use peering connections to transfer data without using the public internet. That is why private IP addresses are used. 

In VPC peering, the Requester is the VPC that initiates a peering connection. As the requester, they will be sending the other VPC an invitation to connect! The acceptor will then be in charge of handling this request. 

![Image](http://learn.nextwork.org/enthusiastic_turquoise_radiant_monstera_deliciosa/uploads/aws-networks-peering_1cbb1b88)

---

## Updating route tables

After accepting a peering connection, my VPCs' route tables need to be updated because we need to define the traffic that goes outbound from the VPC to the peering connection. 

My VPCs' new routes have a destination of the other VPC's CIDR block, with the target being the peering connection. 

ex. for VPC 1, it should target the peering connection with the destination being the CIDR block for VPC 2. 

![Image](http://learn.nextwork.org/enthusiastic_turquoise_radiant_monstera_deliciosa/uploads/aws-networks-peering_4a9e8014)

---

## In the second part of my project...

### Step 5 - Use EC2 Instance Connect

With our instances setup, we'll now use EC2 instance connect and resolve any potential errors. 

### Step 6 - Connect to EC2 Instance 1

After configuring our ec2 instance with an elastic IP address, let's try to connect to our instance again. 

### Step 7 - Test VPC Peering

Now that we're connected to instance 1 , we'll try to send test messages to instance 2. 

---

## Troubleshooting Instance Connect

Next, I used EC2 Instance Connect to ssh into our EC2 instance through the AWS console. 

I was stopped from using EC2 Instance Connect as I realized that we had not auto assigned any public IP addresses to our instance when creating it.

![Image](http://learn.nextwork.org/enthusiastic_turquoise_radiant_monstera_deliciosa/uploads/aws-networks-peering_7685490c)

---

## Elastic IP addresses

To resolve this error, I set up Elastic IP addresses. Elastic IP addresses are a great way to assign an instance a public IPv4 address after launching it. 

Elastic IPs are very popular tools for making sure an application stays available on the internet. Usually, an IP address change means a website's DNS record (i.e. the map that directs users visiting their domain to the right application/server) needs to be updated.

DNS updates take time to propogate across the internet - it can take hours and even days! So without an Elastic IP, a website would be down for its users if an EC2 instance restarts and the engineers have to change a DNS record. With an Elastic IP, the IP address associated with the EC2 instance is always constant - no DNS updates needed!

Associating an Elastic IP address resolved the error because we essentially take a perment public IP from Amazon's pool of addresses and associate it to our instance post creation. 

![Image](http://learn.nextwork.org/enthusiastic_turquoise_radiant_monstera_deliciosa/uploads/aws-networks-peering_45663498)

---

## Troubleshooting ping issues

To test VPC peering, I ran ping with the private IPv4 address of our VPC 2 instance. 

Troubleshooting Notes: 
- Ensure that the instance you're connected to has a security group rule that allows SSH connection. 
- Check to see if the instance you ping to has a security group that allows inbound ICMP messages from our current instance. 

A successful ping test would validate my VPC peering connection because each new line represents a reply from the connection request that we recent. If we continuously get replies, then that means there is successful connectin between our EC2 instances. 

I had to update my second EC2 instance's security group because it was not allowing inbound ICMP messages from our ping command. 

![Image](http://learn.nextwork.org/enthusiastic_turquoise_radiant_monstera_deliciosa/uploads/aws-networks-peering_7a29d352)

---

---
