 # Deleting all S3 buckets with all data using Python...
    Code1.  
      import boto3
      s3 = boto3.resource('s3')
      
      # Get all buckets
      for bucket in s3.buckets.all():
          print(f"Deleting bucket: {bucket.name}")
      
          # Delete all objects (including versions)
          bucket.object_versions.delete()
      
          # Delete bucket
          bucket.delete()
      
      print("All buckets and their data deleted successfully!")

  # code2:
       # -- coding: utf-8 --

        """
        Delete All S3 Buckets (With Full Data Deletion + Confirmation)
        """
        
        import boto3
        import time
        
        s3 = boto3.client("s3")
        
        
        def list_buckets():
            """List all S3 buckets"""
            response = s3.list_buckets()
            return response.get("Buckets", [])
        
        
        def list_all_objects(bucket_name):
            """List all objects inside a bucket"""
            objects = []
            paginator = s3.get_paginator("list_objects_v2")
        
            for page in paginator.paginate(Bucket=bucket_name):
                for obj in page.get("Contents", []):
                    objects.append(obj["Key"])
        
            return objects
        
        
        def delete_all_objects(bucket_name):
            """Delete all objects in batches of 1000"""
            print(f"\n🔹 Deleting objects inside bucket: {bucket_name}")
        
            paginator = s3.get_paginator("list_objects_v2")
        
            for page in paginator.paginate(Bucket=bucket_name):
                objects = page.get("Contents", [])
                if not objects:
                    continue
        
                delete_keys = [{"Key": obj["Key"]} for obj in objects]
        
                s3.delete_objects(
                    Bucket=bucket_name,
                    Delete={"Objects": delete_keys}
                )
        
            # Wait until bucket is empty
            print("⏳ Waiting for bucket to become empty...")
            while True:
                remaining = list_all_objects(bucket_name)
                if not remaining:
                    break
                print(f"Remaining objects: {len(remaining)}")
                time.sleep(5)
        
            print("✅ All objects deleted.")
        
        
        def delete_bucket(bucket_name):
            """Delete empty bucket"""
            s3.delete_bucket(Bucket=bucket_name)
            print(f"🗑 Bucket deleted: {bucket_name}")
        
        
        if _name_ == "_main_":
        
            print("\n🔍 Fetching all S3 buckets...\n")
        
            buckets = list_buckets()
        
            if not buckets:
                print("No buckets found.")
                exit()
        
            for idx, bucket in enumerate(buckets, 1):
                bucket_name = bucket["Name"]
                objects = list_all_objects(bucket_name)
        
                print(f"\n{idx}. Bucket: {bucket_name}")
                print(f"   Objects Count: {len(objects)}")
        
                if objects:
                    print("   Sample Objects:")
                    for obj in objects[:5]:
                        print(f"     - {obj}")
        
            print("\n⚠ WARNING: This will permanently delete ALL buckets and ALL data inside them.\n")
        
            confirm = input("Type 'DELETE ALL BUCKETS' to confirm: ")
        
            if confirm != "DELETE ALL BUCKETS":
                print("❌ Operation Cancelled.")
                exit()
        
            print("\n🚀 Starting Deletion Process...\n")
        
            for bucket in buckets:
                bucket_name = bucket["Name"]
        
                print(f"\n==============================")
                print(f"Processing Bucket: {bucket_name}")
                print(f"==============================")
        
                delete_all_objects(bucket_name)
                delete_bucket(bucket_name)
        
            print("\n🔥 All Buckets Deleted Successfully 🔥")
