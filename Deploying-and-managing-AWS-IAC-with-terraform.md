# Deploying and managing AWS IAC with terraform

In this section you will learn how to authentication a Command Line Interface (CLI) to your AWS account using an AWS profile. This is important because it gives terraform access to your environment and the ability to make changes like adding or deleting resources.

<img width="1622" height="771" alt="image" src="https://github.com/user-attachments/assets/c990dbda-0993-48f0-9a66-d5b330780117" />

1. Run the command:
```bash
cd ~
```
2. Run the command:
```bash
sudo apt update
```
3. Run the command:
```bash
sudo apt install unzip -y
```
4. Run the command:
```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
```
5. Run the command:
```bash
unzip awscliv2.zip
```
6. Run the command:
```bash
sudo ./aws/install
```
7. Return to the Instances tab.
8. In the search bar open IAM in a new tab.
9. Select Users.
10. Click on Create user.
11. Name it `Ecm3_Learner`.
12. Click on Next.
13. Click on Attach policies directly.
14. Attach the policy AmazonS3FullAccess.
15. Click on Next.
16. Click on Create User.
17. Click on your new user.
18. Click on the Security Credentials tab.
19. Click on Create access key.
20. Check Command Line Interface (CLI).
21. Check the box for confirmation.
22. Click on Next.
23. Click on Create access key.
24. Make a copy of the Access Key ID and Secret Access Key.
25. Return to Session Manager.
## usage AWS Sandbox
26. Run the command:
```bash
aws configure 
```
27. Enter the following information when prompted:

    - AWS Access Key ID: <your key>
    - AWS Secret Access Key: <your secret>
    - AWS Token (pour une connexion `ÀWS Sandbox`): <your secret>
    - Default region: `us-east-1`
    - Default output format: `json`

28. Run this command to confirm you are authenticated: 
```bash
aws sts get-caller-identity 
```

This process creates these local files:

- ~/.aws/credentials
- ~/.aws/config

This stores your profile information and your access key information so that you can authenticate to your AWS account through the CLI. This is how terraform gets access to your account to make changes.

---

# Installing and Configuring Terraform using main.tf

In this section you will install terraform and then customize the main.tf file so that you can create an S3 bucket in your AWS environment. The main.tf file is what holds all the information terraform needs to complete a deployment. Here's a summary of the different sections of the main.tf file:

- **provider**: Defines which cloud provider Terraform should use (AWS in this case) and how to connect to it.
- **resource**: This section is where you specify the type of resource you want to create, in this case an aws S3 bucket and you give it a local terraform name, in this case lab_bucket. The format is resource "<provider>_<type>" "<name>".
- **tags**: Optional metadata attached to the resource for organization, filtering, and cost tracking.

1. Run the command:
   - ouvre un nouveau terminal `click sur le signe +`
     
     <img width="207" height="55" alt="image" src="https://github.com/user-attachments/assets/2b5dc8e6-2a98-4f2c-bc94-915cdad3b9df" />

```bash
git clone https://github.com/Yahia-M/Lab-Deploying-and-Managing-AWS-Infrastructure-with-Terraform.git
```
2. Run the command:
```bash
cd Lab-Deploying-and-Managing-AWS-Infrastructure-with-Terraform
```
3. Run the command:
```bash
sudo chmod +x terraform.sh
```
4. Run the command:
```bash
./terraform.sh
```
5. Run the command:
```bash
terraform -version
```
to confirm the installation works. Now you're going to create the main terraform file that will create the resource.
6. Run the command:
```bash
nano main.tf
```
7. In the provider section change profile to "terraform-user" and region to "us-east-1".
8. In the resource section change bucket to something unique, you can use this placeholder and just change the numbers at the end "my-unique-terraform-lab-bucket-12345-[Add some numbers!]". If it's not unique it will tell you at creation and you will need to change it.
9. The tags section is optional and just informational so you can leave that as is. Save and close the file using Control+X, SHIFT+Y and then press enter.
10. Now to prepare for deployment run:
```bash
terraform init
```

In this section you created the terraform file you need to create your S3 bucket and you've downloaded the dependencies you need using terraform init.

---

# Validate and Deploy Infrastructure using Terraform

1. Now run the command:
```bash
terraform plan
```
This will check your current AWS environment against your file and let you know what changes will be made, if any, if you choose to run terraform.
2. Now run the command:
```bash
terraform apply
```
to apply the changes proposed in your terraform file.
3. When prompted, type yes and press enter.
4. To check that the resource was created from the cli run:
```bash
aws s3 ls --profile terraform-user
```
You should now see the S3 bucket.
5. Return to the instances tab.
6. In the search bar open S3 in the new tab. Here you can see the bucket now exists.

Now that you've completed this lab you have demonstrated the ability to authenticate a CLI to an AWS account, configure terraform to create resources in AWS and deployed resources in AWS using terraform plan and terraform apply.
