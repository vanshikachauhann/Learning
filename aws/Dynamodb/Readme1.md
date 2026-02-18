  # Create DynamoDB table from AWS console...

1️⃣ Login to AWS Console <br>
2️⃣ Search → DynamoDB <br>
3️⃣ Click → DynamoDB service<br>
4️⃣ Click → Create table<br>

Fill details: <br>
   Table name: Students<br>
   Partition key: StudentID<br>

Type → String (or Number if you want numeric IDs)

5️⃣ Keep other settings default <br>
6️⃣ Click → Create table <br>

✅ Table created.

 # Delete formate..
   import boto3
from botocore.exceptions import ClientError

# Connect to DynamoDB
dynamodb = boto3.resource('dynamodb', region_name='ap-south-1')
table_name = "Student_Delete"

# ---------- CREATE TABLE ----------
try:
    table = dynamodb.Table(table_name)
    table.load()
    print("Table already exists.")
except ClientError:
    print("Creating new table...")

    table = dynamodb.create_table(
        TableName=table_name,
        KeySchema=[
            {'AttributeName': 'student_id', 'KeyType': 'HASH'}  # Partition Key only
        ],
        AttributeDefinitions=[
            {'AttributeName': 'student_id', 'AttributeType': 'S'}
        ],
        BillingMode='PAY_PER_REQUEST'
    )

    table.wait_until_exists()
    print("Table created successfully!")

table = dynamodb.Table(table_name)

# ---------- INSERT SAMPLE DATA ----------
students = [
    {"student_id": "S1", "name": "Aman", "class": "10th"},
    {"student_id": "S2", "name": "Priya", "class": "9th"},
    {"student_id": "S3", "name": "Rahul", "class": "8th"},
    {"student_id": "S4", "name": "Neha", "class": "10th"},
    {"student_id": "S5", "name": "Arjun", "class": "7th"}
]

for student in students:
    table.put_item(Item=student)

print("\nSample records inserted.\n")

# ---------- SHOW ALL ITEMS ----------
print("Current Table Data:\n")

response = table.scan()
items = response['Items']

for item in items:
    print(item)

# ---------- DELETE BASED ON USER INPUT ----------
delete_id = input("\nEnter student_id to delete: ")

table.delete_item(
    Key={
        'student_id': delete_id
    }
)

print("\nRecord deleted successfully!")

# ---------- SHOW UPDATED TABLE ----------
print("\nUpdated Table Data:\n")

response = table.scan()
items = response['Items']

for item in items:
    print(item)
