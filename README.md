# Automation with CloudFormation

**Create & Configure an EC2 Instance using CFN:**

We know that we'll be creating an EC2 Instance, so lets start by creating a Key Pair. \
We won't be using this Key Pair to connect to the Instance, but it will be required when we apply the CFN template.

\
EC2 → Network & Security → Key Pairs → Create Key Pair\
Name: A4L-Key \
File Format: pem \
Create Key Pair

\
CloudFormation → Create Stack

Prepare Template: Template is ready \
Specify Template: Upload a template file \
Choose File: Locate your ec2instance.yaml template \
Next

Whenever you Upload a template to CloudFormation, it will upload the template to an S3 Bucket that CFN creates automatically. \
You may notice a lot of buckets with the prefix cf- that get created in a region automatically. \
You can tidy things up and delete these if you want to.

Stack name: cfndemo1

Parameters: \
These are the Parameters that are specified within the ec2instance.yaml template! \
The template was written to have dafault values, which is the reason why there are pre-populated fields!

KeyName: A4L-Key \
LatestAmiId: default value \
SSHandWebLocation: default value \
Next

Configure Stack Options: these will be discussed later. \
Next

Review cfndemo1: \
Scroll to bottom

Capabilities: check box to acknowledge \
Create Stack

CFN views some resources it creates as "high risk". We are creating an Identity (IAM Role) \
Because it's an Identity, it's changing something that provides access to AWS, and CFN wants us to explicitly acknowledge that we want to create this resource.

Click the Refresh button to see the status being updated. \
The creation of these Stacks will take a few min. \
The EC2 Instance will be the last component the Stack will create.

Click the Outputs tab \
Notice the Outputs will perfectly match the Outputs that were specified in the yaml template!

The same is true for the Resources tab. \
Click any of the Physical ID's to be redirected to those resources (ex: EC2Instance; InstanceSecurityGroup)

**Create another EC2 Instance using the same YAML template:** \
Create Stack → With new resources (standard)

This is one of the powerful features of CloudFormation. \
Apply the same template multiple times to create the same set of consistant infrastructure! \
We can also apply the same template in other regions

\
\
**Clean Up!!**\
CloudFormation → Stacks \
Select the cfndemo1 Stack → Delete → Delete Stack \
Observe the deletion progress in the Events tab (click Refresh button)

Confirm Deletion: EC2 Instance should be Terminated; Stack should be deleted

This Deletion will delete all of the Logical Resources, and then it deletes all of the corresponding Physical Resources. \
This is another powerful feature. \
CloudFormation cleans up after itself!
