## S3 triggering lambda to update dynamoDB ----

  ✅ What This Architecture Means
       Flow:<br>
             File uploaded to S3 <br>
                   ↓ <br>
             S3 Event Trigger <br>
                   ↓<br>
             Lambda function runs<br>
                   ↓<br>
             Lambda writes/updates item in DynamoDB<br>

## ✅ Step 1 — Create DynamoDB Table

    Example table: 
        Table name: FileMetadata
        Primary key: file_id (String)

##  ✅ Step 2 — Create Lambda Function

Runtime: Python
    Permissions: Lambda must have access to DynamoDB

    Attach IAM policy to Lambda role:
         AmazonDynamoDBFullAccess 

 ##  ✅ Step 3 — Give Permission to Lambda

        Lambda must be allowed to access DynamoDB.
             Lambda → Configuration → Permissions → Role 

 ## ✅ Step 4 — Add S3 Trigger

    Go to Lambda:
    Configuration → Triggers → Add trigger  
    
     Select:
        Source = S3
        Choose bucket
        Event type = ObjectCreated
        Enable trigger ✅
        Now Lambda will run automatically when file is uploaded.   
                     
