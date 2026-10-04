# Secure Multi-Account AWS Organization

This lab takes my existing cross-account lab up to an organizational level.
Here is the lab for reference: https://github.com/masoncyber10/Cross-Account-Lambda-to-S3-Access

## Create an AWS Organization (will upgrade to the AWS Paid Plan)
Search "AWS Organizations" and click on Create AWS Organization

### Create 3 accounts with AWS organization
Add an "AWS account" and make two accounts name under Log Archive and Workload
The Management Account is already created since its your root account
Treat the email accounts like its own email: (email used to create organization + log ) @ gmail.com
Here's an example:   
<img width="316" height="57" alt="image" src="https://github.com/user-attachments/assets/10440258-ef4e-491d-ae53-64f9e0f27ce6" />

## IAM Identity Center
Enable IAM Identity Center with Single Region 

### Create 2 groups (Admin and ReadOnly-Auditors)
Creating the two groups (Admin & ReadOnly-Auditors):
- Click on groups under Dashboard
- Click on create group
- Name the groups (Admin & ReadOnly-Auditors)  
- Create group
<img width="1673" height="719" alt="image" src="https://github.com/user-attachments/assets/f386bf63-d397-4dd2-8644-5e96700658a4" />

#### Assigning Permission Set to Accounts
- Create a permission set --> Use predefined permission set (ViewOnlyAccess) --> Click Next
- Leave next page default and create permission set
- Click on the AWS Accounts
- Check the AWS accounts that you are assigning the groups to
- Log Archive and Workload Accounts --> ReadOnly-Auditors --> Click Next
- Assign the permission set just created by checking the permission set --> Click Submit
- Create another permission set for Admin Access
- Use the predefined permission set and use "Administrative Access"
- Leave next page default and create the permission set
- Assign the new permission set created to the Management account
- Create a permission set for each account
- Turn on Multi-Factor Authentication
- Under prompt users for MFA (default: "Only when their sign-in context changes")
- Change the default option to "Every time they sign in" --> Hit "Save Changes"

<img width="1312" height="582" alt="image" src="https://github.com/user-attachments/assets/7176cca2-f127-4f60-a4d4-4481a02de713" />

## Create Two Users for Admin & Read-Auditor Group
**Create the user for Admin**
- Fill in "Primary Information" according to group
- Assign the user to Admin group
- Add the user

**Create another use for Read-Auditor**
- Fill in "Primary Information" according to group
- Assign user to Read-Auditor group
- Add the user

<img width="2327" height="212" alt="image" src="https://github.com/user-attachments/assets/14378676-b23a-485c-9ee9-38da9e1bde2c" />


## Create 3 Service Control Policies (SCPs)
- Deny cloudtrail:StopLogging / Delete Trail include UpdateTrail and PutEventSelectors
- Deny any region except us-east-1
- Deny leaving the organization

