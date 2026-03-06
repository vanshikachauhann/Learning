# RDS database Automations using python..
    8️⃣ Architecture (Real Flow)
            Python Script
                 ↓
            AWS SDK (boto3)
                 ↓
            RDS Instance
                 ↓
            MySQL Database
                 ↓
             Tables

#### Python code...
          import boto3
          import pymysql
          import time
          
          # ---------- Step 1: Create RDS Instance ----------
          rds = boto3.client('rds')
          
          db_identifier = "mydbinstance3"
          
          print("Creating RDS instance...")
          
          rds.create_db_instance(
              DBInstanceIdentifier=db_identifier,
              AllocatedStorage=20,
              DBInstanceClass='db.t3.micro',
              Engine='mysql',
              MasterUsername='admin',
              MasterUserPassword='Password123',
              PubliclyAccessible=True
          )
          
          # ---------- Step 2: Wait until RDS is available ----------
          print("Waiting for RDS instance to become available...")
          
          waiter = rds.get_waiter('db_instance_available')
          waiter.wait(DBInstanceIdentifier=db_identifier)
          
          print("RDS instance is available")
          
          # ---------- Step 3: Get RDS Endpoint ----------
          response = rds.describe_db_instances(DBInstanceIdentifier=db_identifier)
          
          endpoint = response['DBInstances'][0]['Endpoint']['Address']
          
          print("RDS Endpoint:", endpoint)
          
          # ---------- Step 4: Wait few seconds for DB startup ----------
          time.sleep(30)
          
          # ---------- Step 5: Connect to RDS ----------
          print("Connecting to database...")
          
          connection = pymysql.connect(
              host=endpoint,
              user='admin',
              password='Password123'
          )
          
          cursor = connection.cursor()
          
          print("Connected to RDS")
          
          # ---------- Step 6: Create Database ----------
          cursor.execute("CREATE DATABASE studentdb")
          cursor.execute("USE studentdb")
          
          print("Database created")
          
          # ---------- Step 7: Create Table ----------
          create_table_query = """
          CREATE TABLE students (
              id INT AUTO_INCREMENT PRIMARY KEY,
              name VARCHAR(50),
              age INT
          )
          """
          
          cursor.execute(create_table_query)
          
          print("Table created")
          
          # ---------- Step 8: Insert Data ----------
          insert_query = "INSERT INTO students (name, age) VALUES ('Rahul', 21)"
          
          cursor.execute(insert_query)
          
          connection.commit()
          
          print("Data inserted successfully")
          
          # ---------- Step 9: Fetch Data ----------
          cursor.execute("SELECT * FROM students")
          
          rows = cursor.fetchall()
          
          for row in rows:
              print(row)
          
          connection.close()
          
          print("Process completed successfully")
    

             
