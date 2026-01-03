
**Author:** Cody Chinothai  
**Email:** cchinothai@gmail.com

## Testing VPC Connectivity

![Image](http://learn.nextwork.org/enthusiastic_turquoise_radiant_monstera_deliciosa/uploads/aws-networks-connectivity_8ee57662)

---

## Introducing Today's Project!

Today I Learned: 

⬆️ Connect to your Public Server with EC2 Instance Connect: You used EC2 Instance Connect in your AWS Management Console to securely SSH into your EC2 instance without the hassle of managing SSH keys. This also required a cheeky update to your Public Server's security group settings.

🤝 Test EC2 connectivity with ping: You made sure that your public and private servers can communicate with each other using the ping command. You also had to update your Private Server's NACL settings to make this work!


🛜 Verify VPC internet access with curl: You confirmed that your virtual network can reach the internet by using the curl command to fetch data directly from web servers, even grabbing entire HTML files in the process.


## Connecting to an EC2 Instance

Connectivity is all about how well different parts of your network talk to each other and with external networks.

It's essential because connectivity is how data flows smoothly across your network, powering everything from simple web hosting on the Internet to complex operations e.g. Netflix using over 100,000 EC2 instances to power its streaming platform. 

Solid connectivity is the backbone of any system that relies on network interactions, making every communication and operation reliable and efficient.

My first connectivity test was whether I could connect to our public server via EC2 instance connect. 

![Image](http://learn.nextwork.org/enthusiastic_turquoise_radiant_monstera_deliciosa/uploads/aws-networks-connectivity_88727bef)

---

## EC2 Instance Connect

I connected to my EC2 instance using EC2 Instance Connect, which is an alternate way of SSH into your server via the AWS console. EC2 instance connect will create and manage key pairs for you and simplifies the SSH process. 

My first attempt at getting direct access to my public server resulted in an error, because we looked into our server's security group and realized that it only allowed traffic inflow via HTTP.

I fixed this error by adding a new rule that allowed us to connect via SSH. We specified the IP address as Anywhere-IPv4 for demo purposes but you can make this more restrictive. 

![Image](http://learn.nextwork.org/enthusiastic_turquoise_radiant_monstera_deliciosa/uploads/aws-networks-connectivity_1cbb1b88)

---

## Connectivity Between Servers

ping is the command to test the connectivity between two hosts. We did this to make sure we configured our ec2 instance network correctly. 

While in the instance connect for our public servier, the ping command I ran was ping [privateIPv4 address of our private server]. 

The first ping returned the initiation of a ping connection with no reply. 

Usually, when you ping another computer successfully, you should see several replies back instantly. Each reply tells you how long it took for the message to go to the Private Server and come back.

If you don't get any replies (that's our situation right now), or if the replies stop suddenly, it's usually a sign that there's a problem with the connection. 

![Image](http://learn.nextwork.org/enthusiastic_turquoise_radiant_monstera_deliciosa/uploads/aws-networks-connectivity_defghijk)

---

## Troubleshooting Connectivity

I troubleshooted this error by looking at the Network ACL for our private server and realized that it did not allow ICMP IPv4 traffic, so we added inbound/output rules for the NACL that allowed All ICMP IPv4 with our public subnet's CIDR block as the source. 

I then updated our private server's security group to also allow this ICMP IPv4 traffic.  

![Image](http://learn.nextwork.org/enthusiastic_turquoise_radiant_monstera_deliciosa/uploads/aws-networks-connectivity_4a9e8014)

---

## Connectivity to the Internet

Curl is a command to test network connectivity and also transfar data to/from the server. A normal curl command to a website would return the HTML from that website. 

I used curl to test the connectivity between our public server and the public internet. We can confirm successful connection with this curl command. 

### Ping vs Curl

Ping solely tests connectivity between two servers while curl can send data between the servers using HTTP/HTTPS

---

## Connectivity to the Internet

I ran the curl command curl example.com which retrieved the static HTML content for that site. 

![Image](http://learn.nextwork.org/enthusiastic_turquoise_radiant_monstera_deliciosa/uploads/aws-networks-connectivity_8ee57662)

---

---
