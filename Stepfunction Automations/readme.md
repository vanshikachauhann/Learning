# Flow diagram simple------
                  S3 Upload
                  ↓
              Eventbridge
                  ↓
              Step Function
                  ↓
              Lambda 1 (Insert Metadata in DynamoDB)
                  ↓
              Get SSM Parameter
                  ↓
              Choice State
                 ↙        ↘
              EMAIL      SMS
                ↓          ↓
              SES        SNS
                ↓         ↓
              lambda2    lambda3
                     ↓
                     End

### Now, Explain this step  ---------
  # step1. 
            (a) create bucket...
            (b) Properties ---- Amazon EventBridge

     Send notifications to Amazon EventBridge for all events in this bucket
         On(-)

  # step2.
         Step function....now create static machine
         After that-----
               code--
                  {
        "Comment": "Notification Flow using Lambda + Choice",
        "StartAt": "Lambda1",
        "States": {
          "Lambda1": {
            "Type": "Task",
            "Resource": "arn:aws:lambda:ap-south-1:982081066077:function:Lambda1",
            "Next": "ChoiceState"
          },
          "ChoiceState": {
            "Type": "Choice",
            "Choices": [
              {
                "Variable": "$.notification_type",
                "StringEquals": "ses",
                "Next": "Lambda2"
              },
              {
                "Variable": "$.notification_type",
                "StringEquals": "sns",
                "Next": "Lambda3"
              }
            ],
            "Default": "EndState"
          },
          "Lambda2": {
            "Type": "Task",
            "Resource": "arn:aws:lambda:ap-south-1:982081066077:function:Lambda2",
            "End": true
          },
          "Lambda3": {
            "Type": "Task",
            "Resource": "arn:aws:lambda:ap-south-1:982081066077:function:Lambda3",
            "End": true
          },
          "EndState": {
            "Type": "Succeed"
          }
        }
      }
than,Replace the source name by ARN lambda1,lambda2,lambda3 

<img width="367" height="203" alt="image" src="https://github.com/user-attachments/assets/4b2cfa69-2f30-4ffa-899d-90291e98a76e" />

# step3.
    ## Create function lambda1.
    (a) lambda1 ---- s3 trigger
         (b) code---
                import json
                import boto3
                import os
                
                ssm = boto3.client('ssm')
                
                def lambda_handler(event, context):
                    print("Received input:", json.dumps(event))
                
                    # Get SSM parameter
                    param_name = os.environ.get("SSM_PARAM_NAME", "/xyz") # change the value of parameter
                
                    response = ssm.get_parameter(
                        Name=param_name,
                        WithDecryption=True
                    )
                
                    notification_type = response['Parameter']['Value']
                
                    # Enrich payload
                    event['notification_type'] = notification_type
                
                    print("Updated payload:", json.dumps(event))
                
                    return event

 (c) lambda1 ---- configuration ------permission-----Rolename----- Add permission
         . Amazondynamodbfull access <br>
         .AmazonSSMFull Access <br>


  # step4. 
      (a) create function lambda2..
          import boto3
          import json
          
          ses = boto3.client('ses', region_name='ap-south-1')
          
          SENDER = 'chauhanvanshika707@gmail.com'   # change the  sender emailaddress
          RECIPIENT = 'chauhanvanshika707@gmail.com' # change the reciver emailid 
          
          def lambda_handler(event, context):
              print("SES Event:", json.dumps(event))
          
              subject = "📂 New File Uploaded to S3"
          
              body_text = f"""
          A new file has been uploaded to S3.
          
          Bucket: {event['bucket']}
          File: {event['key']}
          Size: {event['size']} bytes
          Upload Time: {event['event_time']}
          ETag: {event.get('etag', 'N/A')}
          """
          
              response = ses.send_email(
                  Source=SENDER,
                  Destination={
                      'ToAddresses': [RECIPIENT]
                  },
                  Message={
                      'Subject': {'Data': subject},
                      'Body': {
                          'Text': {'Data': body_text}
                      }
                  }
              )
          
              print("SES Response:", response)
          
              return {
                  "status": "email_sent",
                  "messageId": response['MessageId']
              } 
(b) lambda1 ---- configuration ------permission-----Rolename----- Add permission
      (a) AmazonSESFull access.
      
              
 # step 5.
     create lambda3.....
       code....
            import boto3
            import json
            import os
            
            sns = boto3.client('sns', region_name='ap-south-1')
            
            TOPIC_ARN = 'arn:aws:sns:ap-south-1:982081066077:Costname'
            
            def lambda_handler(event, context):
                print("SNS Event:", json.dumps(event))
            
                message = f"""
            New file uploaded to S3
            
            Bucket: {event['bucket']}
            File: {event['key']}
            Size: {event['size']}
            Time: {event['event_time']}
            """
            
                response = sns.publish(
                    TopicArn=TOPIC_ARN,
                    Subject="S3 File Upload Notification",
                    Message=message
                )
            
                print("SNS Response:", response)
            
                return {
                    "status": "sns_sent",
                    "messageId": response['MessageId']
                }

 # step 6 ssm parameters.
      (a) Application tools ----- parameter store -----create parameter <br>
         1. name() <br>
         2.value() /ses or sns ()

 # step7. Eventbridge 
  <img width="914" height="301" alt="image" src="https://github.com/user-attachments/assets/c87893a1-3cc0-4ae9-8c1e-7eff526607c7" />
       than....
 <img width="691" height="271" alt="image" src="https://github.com/user-attachments/assets/adbdf90d-8efd-46cb-addc-6dae8db8de79" />

   ### update the rule 
           


          

              
         

                    

                    
              

        
  
