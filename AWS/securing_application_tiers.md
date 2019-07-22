# Securing Application Tiers

## IAM (AWS Identity and Access Management)

- You should not use the root user for your everyday tasks, even your everyday administrative tasks
- should log in as the root user only to create your first IAM user
- should securely lock away the root user credentials, add multifactor authentication (MFA) to this account, and use the root user credentials only to perform the few administrative tasks where this all-powerful account is required.

### features

- **Shared access to your AWS account**: You can grant other people permission to administer and use resources in your AWS account without having to share your password or access key. You typically do this using roles.

- **Granular permissions**: You can grant different permissions to different people for different resources.

- **Secure access to AWS resources for applications that run on Amazon EC2**: You can use IAM features to securely provide credentials for applications that run on EC2 instances. These credentials provide permissions for your application to access other AWS resources. Once again, this is often accomplished with the roles component in IAM.

- **Multifactor authentication (MFA)**: You can add two-factor authentication to your root account and to individual IAM users for extra security. With MFA, you or your users must provide not only a password or access key to work with your account but also a code from a specially configured device. The most common approach is to use a cell phone to provide the second authentication component.

- **Identity federation**: You can allow users who already have passwords elsewhere to get temporary access to your AWS account.

- **Identity information for assurance**: If you use AWS CloudTrail, you receive log records that include information about those who made requests for resources in your account. That information is based on IAM identities.

- **PCI DSS Compliance**: IAM supports the processing, storage, and transmission of credit card data by a merchant or service provider. It has been validated as being compliant with the Payment Card Industry (PCI) Data Security Standard (DSS).

- **Integration with many AWS services:** IAM can be used across AWS services and resources seamlessly.

- **Eventually consistent:** IAM, like many other AWS services, is eventually consistent. IAM achieves high availability by replicating data across multiple servers within Amazon’s data centers around the world. If a request to change some data is successful, the change is committed and safely stored. However, **the change must be replicated across IAM, which can take some time**. Such changes include creating or updating users, groups, roles, or policies. Amazon recommends that you do not include such IAM changes in the critical, high-availability code paths of your application. Instead, make IAM changes in a separate initialization or setup routine that you run less frequently. Also, be sure to verify that the changes have been propagated before production workflows depend on them.

- **Free use:** IAM and AWS Security Token Service (AWS STS) are features of your AWS account offered at no additional charge.

### Methods to work with it

- AWS Management Console

- AWS command-line tools

- AWS SDKs

- IAM HTTPS API

### IAM Identities

#### User

- An IAM user is an entity that you create in AWS.

- The IAM user represents the person or service that uses the IAM user to interact with AWS
  A user in AWS consists of a name, a password to sign in to the AWS Management Console, and up to two access keys that can be used with the API or CLI.

- When you create an IAM user, you should grant it permissions by making it a member of a group that has appropriate permission policies attached.

- Although you could attach these policies directly to the user account, this approach is usually terrible for scalability in your security design

- In fact, most seasoned AWS administrators use groups even if these groups contain only a single user account.

  > You can clone the permissions of an existing IAM user, which automatically makes the new user a member of the same groups and attaches all the same policies.

#### Group

> A group is not truly an identity because it cannot be identified as a principal in a resource-based or trust policy. It is only a way to attach policies to multiple users at one time
