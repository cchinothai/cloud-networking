
# VPC Traffic Flow and Security

**Author:** Cody Chinothai  
**Email:** cchinothai@gmail.com

---

## VPC Traffic Flow and Security

![Image](http://learn.nextwork.org/enthusiastic_turquoise_radiant_monstera_deliciosa/uploads/aws-networks-security_92b0b0b4)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is your own delegated space within the cloud where you can control your resources and the traffic that flows into them. It's useful to control client/user requests from a cloud security perspective to ensure that you are safely transferring data to and from your resources. 

<img width="1522" height="806" alt="image" src="https://github.com/user-attachments/assets/279f1c56-4232-46b6-8962-cb26d3f71e1c" />


### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to configure our own route tables, security groups, and network ACLs.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was the default route tables, security groups, and network ACLs that were already setup for our existing VPC. 

## Route tables

Route tables map the expected traffic from our resources within our subnet. Think of it like a GPS. Just like a GPS helps people get to their destination in a city, a route table is a table of rules, called routes, that decide where the data in your network should go.

Every subnet in your VPC needs to be linked to a route table, because the table tells your subnet's traffic where to travel to send and receive data. For example, if you have a web server (i.e. an EC2 instance) hosting a website, the EC2 instance's subnet needs a route table that knows how to direct incoming traffic to the website.

<img width="1489" height="825" alt="image" src="https://github.com/user-attachments/assets/fd711796-a8a7-43e7-baf6-baaf95b6a0e4" />



Routes tables are needed to make a subnet public because there must be a defined route from your resources to your internet gateway if you have internet-bound trafiic. 

![Image](http://learn.nextwork.org/enthusiastic_turquoise_radiant_monstera_deliciosa/uploads/aws-networks-security_0a07b191)

---

## Route destination and target

Routes are defined by their destination and target. The destination refers to the IP address it wants to reach, whereas the target is the means that they use to reach that destination. For example, you may want to end up at a destination with a certain IP on the internet, so you target the internet gateway in order to do so. 

The route in my route table that directed internet-bound traffic to my internet gateway had a destination of 0.0.0.0/0 with the target being the internet gateway that we setup for our current VPC.

![Image](http://learn.nextwork.org/enthusiastic_turquoise_radiant_monstera_deliciosa/uploads/aws-networks-security_0a07b191)

---

## Security groups

Security groups define the allowable inbound/outbound traffic for each resource in your subnet. 

If VPCs are cities and subnets are neighbourhoods, a security group is a security checkpoint, or security guard, at the entrance for each building (resource) in that neighbourhood (subnet).

** Note: Network ACLs are stateless and only filter traffic based on rules, while Security groups are stateful and track connections.  

### Inbound vs Outbound rules

Inbound rules are the protocol specifications that are allowed to access your resource. 

If you need your resource to be accessible to the public, you may want to allow inbound connection from any IPV-4 address via an HTTP protocol. 

You can make this more restrictive depending on the use case of your resource. 

Outbound rules are the data that your resources send out. 

Examples of outbound data: Your server requests data from another service; your app sends out an email notification.

By default, AWS allows actions for all outbound data from your resource.  

![Image](http://learn.nextwork.org/enthusiastic_turquoise_radiant_monstera_deliciosa/uploads/aws-networks-security_92b0b0b4)

---

## Network ACLs

Network ACLs are similar to security groups but they operate at the VPC level. 

Think of Network ACLs as traffic cops stationed at every entry and exit point of your subnet, checking each data packet against a table of ACL rules before allowing them through.

<img width="1304" height="830" alt="image" src="https://github.com/user-attachments/assets/4b3d5244-9bb8-45f9-820d-c75288cb32d1" />


### Security groups vs. network ACLs

Security groups operate at a narrower scope - the actual resources themselves. This means that it's within the instance level. Network ACLs on the other hand will apply to all of the subnets in the current VPC (subnet level). 

---

## Default vs Custom Network ACLs

### Similar to security groups, network ACLs use inbound and outbound rules

By default, a network ACL's inbound and outbound rules will allow all traffic, denoted by the (*) rule number. 

In contrast, a custom ACL’s inbound and outbound rules are automatically set to deny all traffic, until you specify by adding a new inbound/outbound rule. 

![Image](http://learn.nextwork.org/enthusiastic_turquoise_radiant_monstera_deliciosa/uploads/aws-networks-security_4faeb056)

---

## Tracking VPC Resources

---

---
