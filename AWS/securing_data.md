# Securing Data

## RESOURCE ACCESS AUTHORIZATION

### Features of EC2 and Identity and Access Management (IAM) to

- Allow other users, services, and applications to use your EC2 resources without sharing your security credentials.

- Control how other users use resources in your AWS account.

- Use security groups to control access to your EC2 instances.

- Allow full use or limited use of your EC2 resources.

### IAM enables you to do the following:

- Create users and groups under your AWS account

- Assign unique security credentials to each user under your AWS account

- Control each user’s permissions to perform tasks using AWS resources

- Allow the users in another AWS account to share your AWS resources

- Create roles for your AWS account and define the users or services that can assume them

- Use existing identities for your enterprise to grant permissions to perform tasks using AWS resources

## STORING AND MANAGING ENCRYPTION KEYS IN THE CLOUD

**AWS Key Management Service (AWS KMS)** is a managed service that makes it easy for you to create and control the encryption keys used to encrypt your data

### Management actions on your AWS KMS master keys

- Create, describe, and list master keys

- Enable and disable master keys

- Create and view grants and access control policies for your master keys

- Enable and disable automatic rotation of the cryptographic material in a master key

- Import cryptographic material into an AWS KMS master key

- Tag your master keys for easier identification, categorizing, and tracking

- Create, delete, list, and update aliases, which are friendly names associated with your master keys

- Delete master keys to complete the key lifecycle

### cryptographic functions using master keys

- Encrypt, decrypt, and re-encrypt data

- Generate data encryption keys that you can export from the service in plaintext or encrypted under a master key that does not leave the service

- Generate random numbers suitable for cryptographic applications

## PROTECTING DATA AT REST

### Three different models for how you and AWS provide the encryption of data at rest and the KMI

- You control the encryption method and the entire KMI.

- You control the encryption method, AWS provides the storage for KMI, and you control the management of the KMI.

- AWS controls the encryption method and the entire KMI.

### Control encryption

- The encryption you engage in with your data at rest might involve S3. You encrypt the data and then upload it to S3 using the S3 API. You can also use the AWS S3 encryption client. You supply the key to this client, and let it encrypt and decrypt the S3 data as part of your call to the S3 bucket.

- You can opt to encrypt EBS volumes that instances use in EC2. Your approach might be at the block level or the file level.

- You can encrypt data that you have on-premises and have this data stored in S3 through an AWS Storage Gateway.

- You can encrypt your data stored in AWS RDS using a variety of approaches. You can also use your encryption in conjunction with AWS Elastic MapReduce. This is the Hadoop implementation in AWS.

## DECOMMISSIONING DATA SECURELY

- **Clear**: Applies logical techniques to sanitize data in all user-addressable storage locations for protection against simple noninvasive data recovery techniques; typically applied through the standard Read and Write commands to the storage device, such as by rewriting with a new value or using a menu option to reset the device to the factory state (where rewriting is not supported).

- **Purge**: Applies physical or logical techniques that render Target Data recovery infeasible using state-of-the-art laboratory techniques.

- **Destroy**: Renders Target Data recovery infeasible using state-of-the-art laboratory techniques and results in the subsequent inability to use the media for storage of data.

## PROTECTING DATA IN TRANSIT

- You can connect to an AWS access point via **HTTP or HTTPS using Secure Sockets Layer (SSL)**. As you most likely know already, HTTPS is a cryptographic protocol that is designed to protect against eavesdropping, tampering, and message forgery.

- For customers who require additional layers of network security, AWS offers the **Virtual Private Cloud (VPC), which provides a private subnet within the AWS cloud**, and the ability to use an IPsec virtual private network (VPN) device to provide an encrypted tunnel between the VPC and your data center

- many AWS customers opt for a **Direct Connect private circuit** for AWS connectivity of data in transit. This solution **focuses on connectivity and not security**. In fact, if encryption is required in this case, an **IPsec tunnel** still needs to be created across the Direct Connect circuit.
