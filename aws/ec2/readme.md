# AWS EC2 (Amazon Elastic computer cloud)..
Amazon Elastic computer cloud is a cloud service that provides resizable virtual servers,called instances,which you can use to run applications.
First Point ..<br>
       Imagine you're running a bussiness and need a server to host your website or appliction.
       Instend of buying and managing physical servers,AWS EC2 lets rent virtual servers in the cloud. These virtual server are called instances.
 Second point ..<br>
        You can Configure several options......<br>
                   .OS <br>
                   .RAM <br>
                   .CPU <br>
                   .Disk/Space <br>
                   .Network/Firewall <br>

 # INSTANCE TYPE:
  Select the hardware capacity (e.g,CPU,Memory).
# AMI(Amazon Machine Image):
Choose the operating system and software(Linux,mac,windows).
# Storage:
Configure the type and size of storage (e.g, EBSvolume ).
# Security Groups:
Set up firewall rules to control inbound/outbound traffic.
# Key Pair:
Create or use an existing key pair for SSH access.
# Network Settings:
Configure VPC,Subnet ,and assign public or private I addresses.
# IAM Role:
Attach an IAM role for permission to access other AWS resoures.
# User Data:
Add scripts to be executed when the instance starts.
# Elastic IP:
Optionally associate a static IP address for consistent public access
# Important points about security groups----
* Region specific<br>
* Only 'Allow' rule (but no deny rule)<br>
* All inbound traffic blocked and outbound allowed by default.<br>
*you define rules for specific:<br>
      Protocol (like HTTP,HTTPS,SSH,etc).
      Port number(e.g,port 22 for SSH)
      IP addresses or range (e.g,allow traffic only from a specific IP or range or IPs)
  *If you allow incoming traffic on a specific port 
   






