# EC2 Instance Automactic start and stop using Aws lambda......
   #### Step1. Ec2 instance create
   #### Step2. IAM Role Permission -----
                * IAM -- Role --CreateRole
                * Permission add --AmazonEc2 full Access
   #### Lambda function create-----
         *AWS ---- Lambda ---- Create function
         *Name --- ?
         *Runtime --- Python
         *Existing role select 
         * Create function

 #### Lambda Code Paste -----
       import boto3

      ec2 = boto3.client('ec2')
      
      INSTANCE_ID = "PASTE-YOUR-INSTANCE-ID"
      
      def lambda_handler(event, context):
      
          action = event.get("action")
      
          if action == "start":
              ec2.start_instances(InstanceIds=[INSTANCE_ID])
              return "EC2 started"
      
          elif action == "stop":
              ec2.stop_instances(InstanceIds=[INSTANCE_ID])
              return "EC2 stopped"
      
          else:
              return "Invalid action"

      * Lambda code paste with instance ID replace karna------Deploy

#### Test Event Create----
    * lambda ---- test ---- Create new event
     JOSN :
##### Start
        {
           "action": "start"
         }
  #### Stop
        {
           "action": "stop"
         }

### Auto Schedule(Event Bridge)
    1.Lambda ------ Add trigger
    2.Choose ------ Event Bridge(schedule)
    3.Rule name   :  ?
    4.Schedul type   ----  rate or cron
    
  
    
                
 
