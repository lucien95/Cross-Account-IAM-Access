# Cross-Account-IAM-Access
Cross-Account-IAM-Access

PROBLEM:

Zalando, an ecommerce business has a multiple AWS accounts environment for development, testing, and production. Working here I noticed that having separate AWS accounts for development, testing, and production. One common challenge they faced was securely sharing product images across these accounts while maintaining control and security.

SOLUTION:

STEPS TO IMPLEMENT:

   - Setup IAM Roles:
        In each AWS account (development, testing, and production), create IAM roles named "ImageSharingRole."

  
  - Configure Trust Relationships:
        In the development account, configure the "ImageSharingRole" to trust the testing and production AWS account IDs. This establishes a trusted relationship(Check the repository for trust relationship policy template and customize) between these accounts.

  - Define Permissions:
        Specify permissions for the "ImageSharingRole" in each account. (You can fine grained permissions based on what you want to achieve and attach to the ROLE.)

  - Apply Resource Policies:
        In the S3 bucket containing product images (located in the production account), apply a resource policy(Check this repository for inline policy which you will create and attach to the ImageSharingRole) that grants access to the "ImageSharingRole" from the development and testing accounts.

  - Test Configuration:
        Test the configuration to ensure that developers and testers in the development and testing accounts can assume the "ImageSharingRole" and access the product images in the production S3 bucket.

BENEFITS OF THIS SOLUTION:

  Security: By using IAM roles with strict permissions, I ensure that only authorized users in the development and testing accounts can access production resources.
  
  Efficiency: This setup allows developers and testers to access production data without the need for duplicating resources in each account, which saves on storage costs.

  Control: You maintain control over who can access and modify the product images. Only users with the necessary permissions can do so.

  Scalability: As Zalando e-commerce business grows, We could easily extend this approach to share other resources, such as databases or APIs, securely across accounts.
