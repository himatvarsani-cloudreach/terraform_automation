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
          aws-region: ${{ secrets.AWS_REGION }}

      - name: git clone my repo
        uses: actions/checkout@v2

      - name: TF ready to go
        uses: hashicorp/setup-terraform@v1

      - name: Init our project
        run: terraform init

      - name: run a plan
        run: terraform plan
