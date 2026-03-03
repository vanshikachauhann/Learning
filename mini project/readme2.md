# Deleting all policy....
   ### code 1...
      import boto3
      iam = boto3.client('iam')
      
      policy_arn = "arn:aws:iam::591292939847:policy/s3readonlyaccess"
      
      # Step 1: Delete Policy
      iam.delete_policy(
          PolicyArn=policy_arn
      )
      
      print("Policy deleted successfully!")


### code 2....
    import boto3
    iam = boto3.client('iam')
    
    # Get all customer managed policies
    paginator = iam.get_paginator('list_policies')
    response_iterator = paginator.paginate(Scope='Local')
    
    for response in response_iterator:
        for policy in response['Policies']:
            policy_arn = policy['Arn']
            print(f"Processing policy: {policy_arn}")
    
            # 1️⃣ Detach from Users
            users = iam.list_entities_for_policy(
                PolicyArn=policy_arn,
                EntityFilter='User'
            )
            for user in users['PolicyUsers']:
                iam.detach_user_policy(
                    UserName=user['UserName'],
                    PolicyArn=policy_arn
                )
                print(f"Detached from user: {user['UserName']}")
    
            # 2️⃣ Detach from Groups
            groups = iam.list_entities_for_policy(
                PolicyArn=policy_arn,
                EntityFilter='Group'
            )
            for group in groups['PolicyGroups']:
                iam.detach_group_policy(
                    GroupName=group['GroupName'],
                    PolicyArn=policy_arn
                )
                print(f"Detached from group: {group['GroupName']}")
    
            # 3️⃣ Detach from Roles
            roles = iam.list_entities_for_policy(
                PolicyArn=policy_arn,
                EntityFilter='Role'
            )
            for role in roles['PolicyRoles']:
                iam.detach_role_policy(
                    RoleName=role['RoleName'],
                    PolicyArn=policy_arn
                )
                print(f"Detached from role: {role['RoleName']}")
    
            # 4️⃣ Delete non-default versions
            versions = iam.list_policy_versions(PolicyArn=policy_arn)
            for version in versions['Versions']:
                if not version['IsDefaultVersion']:
                    iam.delete_policy_version(
                        PolicyArn=policy_arn,
                        VersionId=version['VersionId']
                    )
                    print(f"Deleted version: {version['VersionId']}")
    
            # 5️⃣ Delete the policy
            iam.delete_policy(PolicyArn=policy_arn)
            print(f"Deleted policy: {policy_arn}")
    
    print("All customer managed policies deleted successfully.")
