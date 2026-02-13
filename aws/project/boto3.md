# Create s3 bucket through boto3 python code...
   ### Step 1.   Python installed
  ###  step 2.   boto3 installed → pip install boto3
  ###    step 3.   AWS CLI configured → aws configure (access key, secret key, region)


 # Create S3 bucket with boto3 in python code...
     import boto3
        
           * Create S3 client
        s3 = boto3.client('s3')
        
        bucket_name = "my-unique-bucket-name-12345"   // must be globally unique<br>
        region = "ap-south-1"  # change if needed <br>
        
        try: <br>
            response = s3.create_bucket(<br>
                Bucket=bucket_name,<br>
                CreateBucketConfiguration={<br>
                    'LocationConstraint': region <br>
                } <br>
            ) <br>
            print("Bucket created successfully:", bucket_name) <br>
        
        except Exception as e: <br>
            print("Error:", e)<br>
