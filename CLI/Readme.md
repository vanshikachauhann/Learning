### ✅ How to Create S3 Bucket using AWS CLI
 #####  🔹 Step 1: Configure AWS CLI (if not done)
       (a).aws configure

       It will ask:
          Access Key
          Secret Key
          Region (example: ap-south-1)
          Output format (json)

### 🔹 Step 2: Create Bucket (Basic Command)
  #### aws s3 mb s3://your-bucket-name

  Example: <br>
     aws s3 mb s3://vanshu-test-bucket-123<br>
        make bucket

 ### ✅ How to Create IAM User using AWS CLI
##### 🔹 Step 1: Create IAM User
   ###### aws iam create-user --user-name vanshu-user

If successful, it will return user details in JSON format.

  
