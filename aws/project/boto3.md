# Create s3 bucket through boto3 python code... 
   ### Step 1.   Python installed
  ###  step 2.   boto3 installed → pip install boto3
  ###    step 3.   AWS CLI configured → aws configure (access key, secret key, region)
                  * AWS CLI Install..
                     (a) aws --version
                  * RUN Configure command
                           AWS Access Key ID [None]:
                           AWS Secret Access Key [None]:
                           Default region name [None]:
                           Default output format [None]:

                   * Enter value 
                       (a) Access Key + Secret Key
                          * AWS Console → IAM → Users → Your user → Security credentials → Create access key
                              Access Key ID → paste
                              Secret Access Key → paste
                   * Default Region
                       *ap-south-1   → Mumbai
                        *us-east-1    → N. Virginia 
                   * test configure 
                       * aws s3 ls

                        




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
