# DynamoDB :
DynamoDB stores data as items in tables with each item represnted as a json like documents consisting of key value pairs.
## Serverless:
No need for server provisioning software installation,Maintance or patching.
## Automatic Scaling :
Installing scales up or down based on demands with no manual adjustments windows.
## Zero Downtime :
Provides continuous availability without maintance windows.
## On demand Pricing :
Pay only for the read/write requests used ideal for fluctuating workloads.
## Idle Cost Savings:
Scales down to zero during inactivity,so there no cost when tables have no traffic.
# cloud Front....
It is used to deliver content faster to users by sending data from the nearest server location instead of the main server.
## What CloudFront Delivers
✅ Images<br>
✅ Videos<br>
✅ CSS / JS files<br>
✅ Website content<br>
✅ APIs<br>
✅ Downloads<br>

## How It Works (Flow)
1️⃣ User requests website<br>
2️⃣ Request goes to nearest CloudFront edge location<br>
3️⃣ If cached → served instantly<br>
4️⃣ If not cached → fetched from origin (S3 / EC2 / ALB)<br>
5️⃣ Then cached for next users<br>

## Benefits

Faster content delivery<br>
Low latency<br>
Reduced load on origin server<br>
Better user experience<br>
Global reach<br>

# Route 53
Route 53 is AWS’s DNS (Domain Name System) service.
It is used to connect your domain name to your server or application
Main Functions of Route 53<br>
 1️⃣ Domain Registration<br>
    Buy domain names (.com, .in, .org)<br>
 2️⃣ DNS Routing<br>
    Map domain → EC2 / S3 / Load Balancer / CloudFront<br>
 3️⃣ Health Checks<br>
    Checks if server is healthy<br>
     If not → route traffic to another server<br>

### Example Flow

User types domain → Route 53 DNS → finds IP → browser connects to server.

# AWS-CLI...
   AWS CLI = AWS Command Line Interface

    AWS CLI is a tool that lets you manage AWS services using commands from your terminal / command prompt — instead of using      the AWS web console.

### What You Can Do with AWS CLI

     Using commands you can:<br>

✅ Launch EC2 instances<br>
✅ Create S3 buckets<br>
✅ Upload/download files<br>
✅ Manage IAM users<br>
✅ Create VPC resources<br>
✅ Control RDS, Lambda, CloudFront, etc.<br>

Example..
First step--<br>
  (1) check CLI version<br>
        * aws --version<br>
  (2) configure aws account<br>
        * aws configure<br>
     It will ask:<br>
     * Access Key<br>
     * Secret Key<br>
     * Region<br>
     * Output format<br>
    (3) List S3 buckets<br>
       * aws s3 ls<br>
     (4) Create S3 bucket<br>
        *aws s3 mb s3://my-bucket-name<br>
      (5)Launch EC2 (example)<br>
        *aws ec2 run-instances --image-id ami-xxxx --instance-type t2.micro<br>
     


