### * mini project........
# 1. SQS (Simple queue services ) 

       🏗 Architecture Flow
       
            User Upload File
                    ↓
            S3 Bucket
                    ↓
            Event Notification
                    ↓
            SQS Queue
                    ↓
            Lambda Trigger
                    ↓
            SES (Send Email)

let's start.....
## step1.✅ Step 1: Create S3 Bucket

            Go to S3....
                ↓
            Create bucket
                ↓
            Enable Event Notification (Object Created)

## ✅ Step 2: Configure S3 → SQS

            In S3 bucket:
                Go to Properties
                      ↓
                Event Notification
                      ↓
                Event type: Object Created
                      ↓
                Destination: SQS
                      ↓
                Select queue
                      ↓
  <img width="913" height="197" alt="image" src="https://github.com/user-attachments/assets/b605ac36-96d1-45f3-bbe3-36541620c399" />

                     Now S3 will send metadata to SQS.


            

## ✅ Step 3: Create SQS Queue

        Go to SQS
        Create Standard Queue
  <img width="945" height="134" alt="image" src="https://github.com/user-attachments/assets/bb53c36e-91e7-4098-a6aa-481508e82a1a" />
  <img width="757" height="193" alt="image" src="https://github.com/user-attachments/assets/8e8fa8e0-b254-4a52-beaa-e6bbc8a9ef11" />

  
   ###  make by user policies:
             {
              "Version": "2012-10-17",
              "Statement": [
                {
                  "Sid": "AllowS3SendMessage",
                  "Effect": "Allow",
                  "Principal": {
                    "Service": "s3.amazonaws.com"
                  },
                  "Action": "SQS:SendMessage",
                  "Resource": "arn:aws:sqs:us-east-1:##########:myqueue21",
                  "Condition": {
                    "ArnLike": {
                      "aws:SourceArn": "arn:aws:s3:::sqsbucket"
                    }
                  }
                }
              ]
            }                 
            

        Copy Queue ARN
        Add permission so S3 can send message 

## ✅ Step4 : Create Lambda Function

        Add Trigger:
             ↓
        Choose SQS
             ↓
        Select your queue
<img width="596" height="231" alt="image" src="https://github.com/user-attachments/assets/5616104c-abf1-4b62-919d-989274709595" />

 code ....
  ## ✅ Step 5: Lambda Code (Python)
                    import json
                    import boto3
                    
                ses = boto3.client('ses')
                
                def lambda_handler(event, context):
                    for record in event['Records']:
                        body = json.loads(record['body'])
                        
                        bucket = body['Records'][0]['s3']['bucket']['name']
                        key = body['Records'][0]['s3']['object']['key']
                        
                        subject = "New File Uploaded to S3"
                        message = f"File {key} uploaded in bucket {bucket}"
                        
                        response = ses.send_email(
                            Source='sender@example.com',
                            Destination={
                                'ToAddresses': ['receiver@example.com']
                            },
                            Message={
                                'Subject': {'Data': subject},
                                'Body': {
                                    'Text': {'Data': message}
                                }
                            }
                        )
                        
                    return {
                        'statusCode': 200
                    }

      Replace:
      sender@example.com
      receiver@example.com
      Both must be verified in SES (if sandbox). 


  ## ✅ Step 6: Create SES Setup

            Very important step 🚨
            
            Go to SES
                 ↓
            Verify Email Address
                 ↓
            If account is in sandbox:
                ↓
            Verify sender email
                 ↓
            Verify receiver email also
                 ↓
            Without verification, email will not send.   

        

            
     
   
