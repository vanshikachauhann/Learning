# What is DynamoDB 
   Dynamodb is a serverless NOSQL data by AWS that provide fast and scalable key value and document data storage.
   # Key Features 
     * Serverless  -- no server setup
     * Very fast   -- (millisecond response)
     * Auto Scaling 
     * Highly available
     * Fully managed by AWS 
     * Backup & restore support

# Data Model
  Dynamodb uses:
  * Tables
  * Items(rows)
  * Attributes(columns)

 # Primary Key 
      Every table must have a primary key:
      1. Partition key 
      2. Composite key ( Partition key + Sort key )


# Opertions
  . Putitem - insert 
  . Getitem - read
  . Updateitem  - update
  . Deleteitem - delete
  .Query - search by key
  . Scan - read full table

  ##### Dynamodb vs RDS ..
      Dynamodb = Nosql + serverless + auto scale
      RDS = SQL +relational +managedDB server

   # ✅ Security of DynamoDB Table

         Tables are secured using:
         IAM policies
         Roles
         Encryption at rest
         Encryption in transit
         VPC endpoints 

   # ✅ Backup & Restore

            Enable point-in-time recovery
            Create on-demand backup
            Restore table anytime  

 # ✅ Streams (Real-time changes)

         DynamoDB Streams track:
                  Insert
                  Update
                  Delete
         Used with Lambda for triggers.

 # ✅ TTL (Time To Live)

         Auto delete items after a time.
               Example:
                        Session expires after 1 hour 

# ✅ How You Create Table

         You can create via:
               AWS Console
               AWS CLI
               Python boto3
               CloudFormation
               Terraform

               
                        
    
                      

