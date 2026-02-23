# SNS ((Simple Notification Service) 
    
 
   ## ✅ Step 1: Go to AWS Console
      👉 Search SNS <br>
      👉 Click Simple Notification Service<br>

  ## ✅ Step 2: Click "Create topic"

        You will see two options:
           🔹 Standard <br>
           🔹 FIFO <br>
        👉 Select Standard (for normal use) <br>
             Click Next <br>

 ## ✅ Step 3: Enter Topic Details

            Fill this: <br>
            
                    Name → example: <br>
                    MyFirstSNSTopic <br>
                    Leave other settings default for now <br>
                    Click Create topic <br>
                    
                    🎉 Now your SNS topic is created!<br> 

 ## 📩 Now Add Subscription (SMS)

      Topic alone does nothing. <br>
            You must add Subscription. <br>
      
                  ✅ Step 4: Create Subscription <br>
                          1️⃣ Open your created topic <br>
                          2️⃣ Click Create subscription <br>
                  
                  Fill: <br>
                      Protocol → SMS <br>
                      Endpoint → Your phone number in international format <br>
                      
      Example: <br>
            code : 8974872712  <br>
         Click Create subscription <br>



 # Now,Create S3 Bucket
          1️⃣ AWS Console open karo
          2️⃣ Search karo S3
          3️⃣ Click Create bucket
          
          Fill details:   
               Bucket name → globally unique hona chahiye
          Example:
              vanshu-bucket-2026
      . Region → ap-south-1 (Mumbai) choose kar sakte ho
          Baaki settings default rehne do.

          👉 Click Create bucket

  # ✅ Step 2: Upload File in S3

            1️⃣ Bucket open karo
            2️⃣ Click Upload
            3️⃣ Click Add files
            4️⃣ File select karo
            5️⃣ Click Upload
            
            Ab file S3 me store ho gayi ☁️

  # ✅ Step 1: Create Lambda Function

          1️⃣ AWS Console open karo
          2️⃣ Search Lambda
          3️⃣ Click Create function
Choose:
          ✔ Author from scratch
          Function name → MyFirstLambda
          Runtime → Python 3.12 (latest available)
          Architecture → x86_64 (default)
          
             Click Create function
        🎉 Lambda create ho gayi.

# ✅ Step 2: Understand Lambda Structure  
               import boto3
              import urllib.parse
              from datetime import datetime
              
              # Region MUST be same as SNS
              sns = boto3.client('sns', region_name='ap-south-1')
              
              TOPIC_ARN = "arn:aws:sns:ap-south-1:982081066077:Costname"
              
              def lambda_handler(event, context):
              
                  print("Event Received:", event)
              
                  for record in event['Records']:
              
                      bucket = record['s3']['bucket']['name']
                      key = urllib.parse.unquote_plus(record['s3']['object']['key'])
                      timestamp = datetime.utcnow().strftime("%Y-%m-%d %H:%M:%S")
              
                      message = f"""
              S3 Upload Alert!
              
              File   : {key}
              Bucket : {bucket}
              Time   : {timestamp} UTC
              """
                      print("Publishing started")
                      response = sns.publish(
                          TopicArn=TOPIC_ARN,
                          Message=message,
              
                          # Required for SMS delivery in India
                          MessageAttributes={
                              'AWS.SNS.SMS.SMSType': {
                                  'DataType': 'String',
                                  'StringValue': 'Transactional'
                              },
                              'AWS.SNS.SMS.SenderID': {
                                  'DataType': 'String',
                                  'StringValue': 'S3ALRT'
                              }
                          }
                      )

# S3 → Lambda Trigger
      Flow:
            File upload in S3
            ↓
            Lambda automatically run

      Steps:
            Go to S3 bucket
            Properties
            Event Notifications
            Create event
            Select event type → "All object create events"
            Destination → Lambda
            Choose your Lambda function
            Save.
            Now jab file upload hogi → Lambda run hoga 🚀
          
         
            
