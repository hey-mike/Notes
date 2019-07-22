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

An IAM group is a collection of IAM users. You can use groups to specify permissions for a collection of users, which can make those permissions easier to manage for those users

> A group is not truly an identity because it cannot be identified as a principal in a resource-based or trust policy. It is only a way to attach policies to multiple users at one time

#### Role

- An IAM role is similar to a user, in that it is an identity with permission policies that determine what the identity can and cannot do in AWS
- A role does not have any credentials associated with it. Instead of being uniquely associated with one person, a role is intended to be assumable by anyone who needs it.
- An IAM user can assume a role to temporarily take on different permissions for a specific task
- A role can be assigned to a federated user who signs in by using an external identity provider instead of IAM. AWS uses details passed by the identity provider to determine which role is mapped to the federated user.

#### Policies

- **Identity-based policies**: These policies are attached to users, groups, or roles.

- **Resource-based policies**: These policies are attached to resources in AWS such as S3 buckets.

- **Organization SCPs**: These policies allow the creation of a Service Control Policy (SCP); this permits you to define a permissions boundary to an AWS organization or organizational unit (OU).

- **Access control lists (ACLs)**: These lists control what principals (users/roles/groups) can access a resource; this is the only policy type that does not use a JSON policy document structure.

## SECURING THE OS AND APPLICATIONS

### Security Groups

- Security groups apply to network interfaces to control access to EC2 instances (and potentially other AWS resources).

- Security groups are stateful in their operation; for example, a traffic flow explicitly permitted outbound will trigger a dynamic inbound permission of the return flow for that communication requirement.

- Security groups are built by your PERMIT entries. With security groups, you do not create DENY entries.

- You can reference other security groups from your VPC in your security group; you can also reference security groups in other VPCs that you have peered with.

### Network ACLs

- Network ACLs apply to subnets to control traffic in and out of these subnets.

- Network ACLs are stateless in their operation; you must explicitly permit return flows based on flows permitted in the opposite direction.

- You can use PERMIT and DENY entries with your network ACLs.

- Network ACL entries are processed in order, and order is critically important.

### Systems Manager Patch Manager

AWS Systems Manager Patch Manager automates the process of patching managed instances with security-related updates

- Patch Manager uses patch baselines, which include rules for auto-approving patches within days of their release, as well as a list of approved and rejected patches.
- Patch Manager integrates with IAM, CloudTrail, and CloudWatch events to provide a secure patching experience that includes event notifications and the ability to audit usage
