## How to Configure an Auto Scaling Group Without a Load Balancer....
   ### Step 1: Create a Launch Template

            Go to AWS Console
                Open EC2
                Click Launch Templates
                Click Create Launch Template
            Select:
                AMI
                Instance type
                Key pair
                Security group
                Click Create Launch Template

<img width="772" height="173" alt="image" src="https://github.com/user-attachments/assets/16b8a0e3-cd7c-4a66-9c1a-a57ddfbb8c9d" />

### Step 2: Create Auto Scaling Group

        Go to EC2 Dashboard
        Click Auto Scaling Groups
        Click Create Auto Scaling Group
        Enter Auto Scaling Group Name
        Select the Launch Template

<img width="732" height="332" alt="image" src="https://github.com/user-attachments/assets/f58bc9b9-10e2-460f-b126-42904e1f91c0" />

### Step 3: Choose Network

      Select VPC
      Select Subnets
      Skip Load Balancer (do not attach any)
      
 ### Step 4: Configure Group Size
    Set:
        Minimum capacity → 1
        Desired capacity → 2
        Maximum capacity → 4
  This means at least 1 instance will always run.

### Step 5: Configure Scaling Policy
     Example policy:
        If CPU > 70% → Add 1 instance
        If CPU < 30% → Remove 1 instance
      This uses CloudWatch metrics.

### Step 6: Review and Create

    Click Create Auto Scaling Group.
Now AWS will automatically create or terminate EC2 instances based on the policy, even without a load balancer.     

# Nom,Result.....
<img width="767" height="200" alt="image" src="https://github.com/user-attachments/assets/8ccb7f79-14e6-41bf-b8ce-b25bd507ad02" />

             
