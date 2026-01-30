# IAM...
        IAM is a service that helps you securely control access to AWS resources.
        It allows you to manage users,roles,and permissions to define who can access what within your AWS environment.

 *Free Service : IAM is offered at no additional cost .<br>
 *Global Service<br>
 *Root account created by default,shouldern't be used or shared.<br>

 # Create Users:
   You can create individual user accounts for people who need access to your AWS resources.
 # Assign Permissions: 
   you can assign specific permission to users,groups,or roles to control what action they can perform on AWS services.
 # Create Groups:
   you can group users together and assign permission to the group,making management easier for multiple users.
 # Create Roles:              
   You can create roles to assign temporary permissions to AWS services or users,especially useful for securely managing permissions across different AWS resources.
  # Manage Federated Access:
    IAM allowing allows integrating with external identity prviders (like Active Directory) for centralized management of user access across AWS.   
                     
  # MFA-----
MFA(Multi-Factor Authentication)is an extra layer of security that requires users to provide two or more forms of verifiction like a password and a code from their phone,to access their accounts.
        username + password + security code 
. The AWS Management Console provide a graphical,web-based approach.
. The AWS CLI provider a command-line,scripting approach.
. Aws SDKs and integrate AWS directly into their applications.

# AWS IAM IMPORTANTS POINTS.
     . Avoid using root account except of account setup.
     . Add user to a group and assign permission to group
     . Use password policy or MFA
     . Use Access KEY for CLI/SDK
     . Never share ACCESS KEYS or password
     . Audit the permission using IAM credential report.

















               
