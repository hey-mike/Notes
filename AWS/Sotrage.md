# AWS Storage

## Simple Storage Service (S3)

### S3 Storage Classes

1. Standard

   - Durability of 99.999999999 percent across at least three facilities
   - Low latency
   - Resiliency in the event of entire AZ destruction
   - 99.99 percent availability
   - An SLA governing performance
   - Encryption of in-transit and at-rest data (optional)
   - Lifecycle management (optional)

2. Standard-Infrequent Access

   - Many of the S3 standard features, such as incredible durability
   - Designed for less frequent access but still provides responsiveness
   - An ideal class for workloads like backups
   - Designed for 99.9 percent availability

3. One Zone-Infrequent Access

   - This might be an ideal class for objects like secondary backup copies of data.
   - The objects in this storage class could be replicated to another region should the need arise to increase the availability.
   - As you would guess, availability here is reduced slightly and is designed for 99.5 percent.
   - **There is a risk of data loss in the event of an AZ’s destruction.**

4. Glacier

   - This is an ideal storage class for the archiving of data.
   - Access times to archived data can be from minutes to hours depending on your configuration and purchase plan.

## Elastic Block Store (EBS)

### EBS VS Instance Stores

When using instance stores, you cannot stop and start your EC2 instances. You can only create and terminate (delete) them.

## Elastic File Service (EFS)

It is the AWS managed solution you could use. Like S3, EFS can be scaled easily as needs require.To experiment with EFS, you should consider an Amazon Linux AMI because it has built-in NFS capabilities. This eliminates the need to install NFS separately. **Be sure to permit NFS in the security group used by your EC2 instances that are going to call** on the EFS file system

## GLACIER SERVICES

AWS Glacier is technically part of S3, but you should note there are many fundamental differences. Sure, it gives us 11 nines of durability like the other classes of S3, but there are more differences than similarities. Here are some of the critical unique characteristics you need to be aware of:

- It is specially designed for backup and archiving.
- ZIPs and TARs that you store in Glacier can be huge—up to 40 TBs in size, so here you shatter size limitations of other classes.
- You will be charged more if you find that you are accessing Glacier data more frequently.
- You create Vaults inside Glacier for storage.
- You can create 1,000 Vaults per AWS root account, but this number can be negotiated with Amazon.
- The Archive ID (naming) of stored objects is automated by AWS.
- Like S3, security compliance is an option for a variety of different regulations and standards.
- Amazon does not provide a GUI for the transfer of objects in and out of your Vaults.
- You use the CLI or an SDK or a Lifecycle Policy to transfer objects.
