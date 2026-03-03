# Deleting all lambda  using Python....
    # -- coding: utf-8 --

          import boto3
          import json
          import zipfile
          import time
          import os
          from botocore.exceptions import ClientError
          
          # ==========================
          # CONFIGURATION
          # ==========================
          role_name = "Auto-vscode-lambda-role"
          function_name = "Auto-vscode-lambda"
          runtime = "python3.9"
          region = "ap-south-1"
          
          # ==========================
          # CREATE CLIENTS
          # ==========================
          iam = boto3.client("iam")
          lambda_client = boto3.client("lambda", region_name=region)
          
          print("🔹 Starting Full Lambda Automation...\n")
          
          # ==========================
          # STEP 1: CREATE OR GET IAM ROLE
          # ==========================
          assume_role_policy = {
              "Version": "2012-10-17",
              "Statement": [
                  {
                      "Effect": "Allow",
                      "Principal": {"Service": "lambda.amazonaws.com"},
                      "Action": "sts:AssumeRole"
                  }
              ]
          }
          
          try:
              print("🔹 Creating IAM Role...")
              role = iam.create_role(
                  RoleName=role_name,
                  AssumeRolePolicyDocument=json.dumps(assume_role_policy)
              )
              print("✅ IAM Role Created")
          
          except iam.exceptions.EntityAlreadyExistsException:
              print("⚠ IAM Role Already Exists")
              role = iam.get_role(RoleName=role_name)
          
          # Attach CloudWatch Logs Policy
          try:
              iam.attach_role_policy(
                  RoleName=role_name,
                  PolicyArn="arn:aws:iam::aws:policy/service-role/AWSLambdaBasicExecutionRole"
              )
              print("✅ Policy Attached")
          except ClientError:
              print("⚠ Policy Already Attached")
          
          print("⏳ Waiting for IAM propagation...\n")
          time.sleep(10)
          
          # ==========================
          # STEP 2: CREATE LAMBDA CODE FILE
          # ==========================
          print("🔹 Creating Lambda code file...")
          
          lambda_code = """
          def lambda_handler(event, context):
              return {
                  "statusCode": 200,
                  "body": "Hello Bhai - Full Automation Success"
              }
          """
          
          with open("lambda_function.py", "w", encoding="utf-8") as f:
              f.write(lambda_code)
          
          # ==========================
          # STEP 3: ZIP LAMBDA FILE
          # ==========================
          print("🔹 Zipping Lambda file...")
          
          zip_filename = "lambda.zip"
          
          with zipfile.ZipFile(zip_filename, "w") as zipf:
              zipf.write("lambda_function.py")
          
          # ==========================
          # STEP 4: CREATE OR UPDATE LAMBDA
          # ==========================
          print("🔹 Creating or Updating Lambda...")
          
          with open(zip_filename, "rb") as f:
              zipped_code = f.read()
          
          try:
              response = lambda_client.create_function(
                  FunctionName=function_name,
                  Runtime=runtime,
                  Role=role["Role"]["Arn"],
                  Handler="lambda_function.lambda_handler",
                  Code={"ZipFile": zipped_code},
                  Timeout=15,
                  MemorySize=128,
                  Publish=True,
              )
              print("✅ Lambda Created Successfully 🚀")
          
          except lambda_client.exceptions.ResourceConflictException:
              print("⚠ Lambda Already Exists — Updating Code...")
          
              lambda_client.update_function_code(
                  FunctionName=function_name,
                  ZipFile=zipped_code,
                  Publish=True
              )
          
              print("✅ Lambda Code Updated")
          
          # ==========================
          # STEP 5: WAIT UNTIL LAMBDA ACTIVE
          # ==========================
          print("⏳ Waiting for Lambda to become ACTIVE...")
          
          waiter = lambda_client.get_waiter("function_active_v2")
          waiter.wait(FunctionName=function_name)
          
          print("✅ Lambda is ACTIVE\n")
          
          # ==========================
          # STEP 6: INVOKE LAMBDA
          # ==========================
          print("🔹 Invoking Lambda...")
          
          response = lambda_client.invoke(
              FunctionName=function_name,
              InvocationType="RequestResponse"
          )
          
          result = response["Payload"].read().decode()
          
          print("✅ Lambda Response:")
          print(result)
          
          print("\n🔥 ALL DONE SUCCESSFULLY 🔥")
          
          # ==========================
          # STEP 7: CLEAN LOCAL FILES
          # ==========================
          os.remove("lambda_function.py")
          os.remove("lambda.zip")
          
          print("🧹 Temporary files cleaned")
