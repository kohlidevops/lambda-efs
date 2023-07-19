# lambda-efs
To access the EFS access point through the Amazon Lambda Function

Step -1 : To create a Elastic Filesystem
Firstly create a Filesystem with standard storage class
![efs-creation-1](https://github.com/kohlidevops/lambda-efs/assets/100069489/2a747365-ca58-4909-bb4c-4535557d67f6)

Select the Throughput mode as Enhanced which has two options, Elastic and Provisioned. Elastic is used when workloads with unpredictable IO.
![efs-creation-2](https://github.com/kohlidevops/lambda-efs/assets/100069489/77e4e4ae-7cbd-4fe7-8c9f-66b5c806692f)

Step -2 : Select your VPC and subnets with all availability zones.

The EFS and Lambda should be in a same VPC. The VPC's are different then we need to configure VPC Peering between two VPC's.
![efs-creation-3](https://github.com/kohlidevops/lambda-efs/assets/100069489/27f1048c-6401-420c-8d15-d0d667419369)

Then create a Elastic Filesystem. We will create a EFS access point later.

Step -3: Create IAM Role for Lambda Function

To create a IAM role with below policies to access the Elastic Filesystem accesspoint from Lambda Function.
![efs-iam-1](https://github.com/kohlidevops/lambda-efs/assets/100069489/e980f3b1-af0f-42ad-a32f-9a32b314e45b)

![efs-iam-2](https://github.com/kohlidevops/lambda-efs/assets/100069489/3dbac273-26ff-4928-b2f7-b30496563275)

Step -4: To create a access point for Elastic Filesystem

Navigate to EFS and select your EFS then choose access point to create a new access point
![accesspoint-1](https://github.com/kohlidevops/lambda-efs/assets/100069489/147b691e-a156-46d0-b582-825840f395a9)

Configure the POSIX User and Group ID
![accesspoint-2](https://github.com/kohlidevops/lambda-efs/assets/100069489/02878de4-f27b-4794-99e1-e67402be2bb1)

Configure the permissions for the root directory
![accesspoint-3](https://github.com/kohlidevops/lambda-efs/assets/100069489/33034df9-5da6-4b7f-b5af-c618370d8800)

Then create a access point for Elastic Filesystem
![accesspoint-4](https://github.com/kohlidevops/lambda-efs/assets/100069489/00bb4004-e383-41b7-a941-4c515a5b1e2c)

Step -5: To create a Lambda Function

To create a Lambda Function with Python runtime and associated the IAM role which is created just now.
![lambda-efs-1](https://github.com/kohlidevops/lambda-efs/assets/100069489/24dd7d02-96c7-41ae-9260-00b549cf7c31)

To enable a VPC in Advanced settings and select your VPC and available subnets.
![lambda-efs-2](https://github.com/kohlidevops/lambda-efs/assets/100069489/04b97ad4-f552-4fb4-bd38-49165acee2c1)

Configure the Security group for Lambda Function. Tight your security group with valid source.
![lambda-efs-sg](https://github.com/kohlidevops/lambda-efs/assets/100069489/98ed5065-9b64-4b5c-b880-56511fff70f6)

Deploy the below code in Lambda and dont forget to deploy once code has been updated
![lambda-function-code](https://github.com/kohlidevops/lambda-efs/assets/100069489/e26b430e-fb1a-431c-9584-9f7861b37e93)

Step -6: To associate the EFS access point in Lambda Function

![lambda-efs-add](https://github.com/kohlidevops/lambda-efs/assets/100069489/d3fd9118-4ada-4732-a570-10bca25c4b96)

Make ensure to add the prefix /mnt/ before the access point. In our case, /mnt/access

Step -7: To test the Function
To create sample test event and trigger the function
![lambda-test](https://github.com/kohlidevops/lambda-efs/assets/100069489/174aefce-640d-4d64-99db-058b407cbb24)
