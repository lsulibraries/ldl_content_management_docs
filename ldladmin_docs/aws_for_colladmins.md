# AWS for Collection Admins

## Creating an AWS Account for Collection Admins (as a SysAdmin)

See [Amazon's Documentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html?icmpid=docs_iam_console#id_users_create_console)

1. Go to https://console.aws.amazon.com/iam/.
1. Enter lsulibraries as the account name.
1. Enter username and password
1. Choose Users, then Add user.
1. Enter a user name, preferably corresponding to their Islandora user name.
1. Select AWS Management Console access, autogenerate a password, and require password reset.
1. Add the user to the group ldl-collection-admins  
1. Create the user and make note of the user name and password, to send in an email.  
1. Go to S3 / luslibraries-ldl-for-ingest; if they do not already have a folder for their institution, create one.  

## Instructions for Collection Admins (email this to CA)

To access AWS and upload your files:  

1. Go to https://lsulibraries.signin.aws.amazon.com/console
1. The Account ID should be lsulibraries
1. Username: {username}
1. Password: (I will send this in a separate email; please change this once you log in)
1. You’ll see a big menu of AWS services; under Storage, go to S3
1. Click on the bucket lsulibraries-ldl-for-ingest
1. Click on the folder for {institution}
1. Click the Upload button
Look for the other email momentarily; otherwise, let me know if you get stuck!

## Getting CA-uploaded files from AWS for processing with MIK

1. Go to S3 and navigate to the lsulibraries-ldl-for-ingest folder to verify the items & number.
1. Open Powershell and cd to G:
1. `aws configure`  
    Access Key ID {get from site admin}  
    SAK {get from site admin}  
1. Use:  
`aws s3 cp s3://lsulibraries-ldl-for-ingest/{foldername}/ G:\{remainder_of_path} --recursive`  
    - use double quotes for paths with spaces in S3  
1. Process collection with MIK  
1. Zip ingest package and upload to institution folder
1. Let collection admin know they can pick it up and batch ingest it (create container if needed)
