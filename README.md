# lambda_practice_1# terraform_automation

###### 1. Open VsCode with the terraform files that you would like to automate
###### 2. Create a new directory/folder name it **.github/workflows** in VSCode
###### 3. create a file named **[filename].yml**. 
###### 4. copy the template from - https://docs.github.com/en/actions/quickstart

###### sample code for terraform automation


name: Terraform deployment with Github Actions</br>
on: [push]
jobs:
  terraform-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: AWS authentication
        uses: aws-actions/configure-aws-credentials@v1
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: eu-west-1

      - name: git clone my repo
        uses: actions/checkout@v2

      - name: TF ready to go
        uses: hashicorp/setup-terraform@v1

      - name: Init our project
        run: terraform init

      - name: run a plan
        run: terraform plan
        

### AWS Management Console
IAM --> Users --> Create a temporary user: github-actions
Provide full access (SELECT):
- AmazonS3FullAccess
- AmazonDynomoDBFullAccess
- AmaxonVPCFullAccess
- AmaxonLambdaFullAccess
- IAMFullAccess

Copy the **Access and Security Key** from the security credential tab
copy the user arn and copy it to the yml file 


### GitHub Action
Go to your repository ---> Settings --->Secrets
New repository secret
Name : AWS_ACCESS_KEY

ACCESS KEY
Copy the access key from the IAM Management Console
Paste it under Value: [Access Key]
[Add Secret]

Name : AWS_SECRET_ACCESS_KEY

SECRET ACCESS KEY
Copy the access key from the IAM Management Console
Paste it under Value: [AWS_SECRET_ACCESS_KEY]
[Add Secret]

.git add .
git status
git push


