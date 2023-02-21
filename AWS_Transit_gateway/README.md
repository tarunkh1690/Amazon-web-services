## AWS_Transit_gateway

By following steps we are going to create a transit gateway to connect multiple VPC in the same or multiple aws account without vpc peering.
<br><br>
<img src = "images/tg.png" width = 1200 height =600>
<br><br>


To create TG, I will create 3 VPCs and 3 ec2 instances 1 in each VPC to check.
<br><br>
Step 1: Create VPC Test-TG1, Test-TG12 and Test-TG3 with CIDR 10.1.1.0/24, 10.1.2.0/24 and 10.1.3.0/24 respectively.
<br><br>
<img src = "images/vpc.png" width = 1500 height =200>
<br><br>
Step 2: Now create a subnet for each VPCs, Create 1 public and 1 private subnet in each subnet. I used subnetting to divide CIDR into subnets like 10.1.1.0/25(public)  and 10.1.1.128/25(private).
<br><br>
Step 3: Now create an internet gateway for each VPC, To access ec2 instances now create an internet gateway and attach it to each VPC respectively.
<br><br>
Step 4: Now create 1 EC2 instance in each VPC to check connectivity between servers in different VPC. I have created 2 EC2 (VPC1 & VPC2) in public and 1 EC2 (VPC3) in private to check private subnet ec2 is also accessible from public subnet in different VPC. 
<img src = "images/vpc1-ec2.png" width = 1000 height =300><img src = "images/vpc2-ec2.png" width = 1000 height =300><img src = "images/vpc3-ec2.png" width = 1000 height =300>
<br><br>
Step 5: Now login to each servers and check connectivity by using ping command. I did from VPC1 EC2 and got following response.
<br><br>
Note: You need to allow Custom-ICMP for ping in your security group to check ping response. To enable ICMP protocol (ping response) follow below steps.
<p>Go to EC2 Dashboard and click "Running Instances"</p>
<p>on "Security Groups", select the group of your instance which you need to add security.</p>
<p>click on the "Inbound" tab</p>
<p>Click "Edit" Button (It will open a popup window)</p>
<p>click "Add Rule"</p>
<p>Select the "Custom ICMP rule - IPv4" as Type</p>
<p>Select "Echo Request" as the Protocol (Port Range by default show as "N/A)</p>
<p>Enter the "0.0.0.0/0" as Source</p>
<p>Click "Save"</p>
<img src = "images/connectivity-check-before-tg.png" width = 800 height =300>

<br><br>
Now we need to create Transit Gateway and Transit Gateway Attachment to Solve this problum. Once we will create TG and TG attachment TG route table will create autometiclly with association and propagation for all 3 VPCs.   
<br><br>
Step 6: To create TG go to VPC service at the 


