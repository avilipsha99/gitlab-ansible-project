# GITLAB CI/CD using Terraform: Managing infrastructure

## Content:
 1: creating an IAM user <br>
 2: Creating Gitlab Account <br>
 3: Terraform Files <br>
 4: Variables setup in Gitlab (Secrets) <br>
 5: GitLab CI/CD configuration <br>
 6: .gitlab-ci.yml <br>
 7: Destroy <br>

### Step 1: IAM User creation
1.Navigate to the AWS console.<br>
2.Search for IAM and click "Users."<br>
3.Add a new user.<br>
4.Attach the "AdministratorAccess" policy.<br>
5.Go to security credentials and create access key for the user and also download .csv file.<br>

### Step 2: Gitlab Account
Register for the account or click on github option for creating an account.

### Step 3: Creating terraform Files
Create a blank repository on GitLab and add the following Terraform files: <br>
main.tf: Defines AWS resources.<br>
provider.tf: Configures the AWS provider.<br>
install_jenkins.sh: Shell script for Jenkins installation.<br>
   Here we specify the github repo, where the data will be feteched while installing jenkins.<br>
   **https://github.com/avilipsha99/gitlab-ansible-project.git** <br>
backend.tf: Configures Terraform backend.<br>

### Step 4: Setting up variables/Secrets
Go to Settings -> CI/CD.<br>
Expand the variables section.<br>
Add the following variables with corresponding values:<br>
AWS_ACCESS_KEY_ID<br>
AWS_SECRET_ACCESS_KEY<br>
Keys are now added to this repo.<br>

### Step 5: GitLab CI/CD configuration
here, we specify various stage to run and validate the pipeline with the parameters:<br>
1. validate<br>
2. plan<br>
3. apply<br>
4. stage<br>

Specify the image as well:<br>
Docker image to use for the GitLab Runner. In this project, we have used "hashicorp/terraform:light" image for running Terraform commands. <br>

Also, we specify few commands that runs before each job in the pipeline:<br>
1. export AWS_ACCESS_KEY=${AWS_ACCESS_KEY_ID}<br>
2. export AWS_SECRET_ACCESS_KEY=${AWS_SECRET_ACCESS_KEY}<br>
3. rm -rf .terraform<br>
4. terraform --version<br>
5. terraform init<br>

### Step 6: Creating .gitlab-ci.yml
Refer to .gitlab-ci.yml configuration provided in the repository.<br>
Once terraform apply job is completed.<br>
![image](https://github.com/avilipsha99/gitlab-ansible-project/assets/114740673/079ebb57-e0c0-47d8-8089-fb10128faa6d) <br>

 -Go to aws console --> connect the instance and run the following commands in order to integrate with jenkins:<br>
  -cd /<br>
  -ls -lrt<br>
  -cd Ansible  (mkdir used in shell script)<br>
  -cd gitlab-ansible-project (cloned repo)<br>
  -ls  (here we will find the files present in github repo i.e Jenkins-EC2, Jenkinsfile, Jenkins-playbook.yml ,ec2.yml, Readme.md)<br>
  -cd /home/ubuntu<br>
  -cd /var/log/<br>
  -ls<br>
  -cat user-data.log (here, we ll find all the software that was required for installing jenkins along with jenkins has been  installed)<br>
  -Copy the public IP of the ec2 instance and append it with 8080 port and connect by providing the password.<br>
  ![image](https://github.com/avilipsha99/gitlab-ansible-project/assets/114740673/9e2852bb-06e5-4721-a8aa-8fce27d2cce8) <br>
  ![image](https://github.com/avilipsha99/gitlab-ansible-project/assets/114740673/70327957-be58-44bd-a1be-8c7dfaee9e78) <br>
  ![image](https://github.com/avilipsha99/gitlab-ansible-project/assets/114740673/409008f1-7383-4c1f-8d80-ec15eca407f0) <br>
  ![image](https://github.com/avilipsha99/gitlab-ansible-project/assets/114740673/0aac7941-bd11-4a46-8228-f77d1103cf38) <br>





### Step 7: Destroy stage
We need to manually provide destroy to delete resources.<br>
![image](https://github.com/avilipsha99/gitlab-ansible-project/assets/114740673/a8843db0-59ac-4730-9f61-102036de2cf6)














```



