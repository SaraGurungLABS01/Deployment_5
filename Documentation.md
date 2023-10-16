## Purpose

The purpose of this project is to demonstrate the end-to-end deployment of a highly available and secure web application infrastructure using Terraform, AWS services, and Jenkins automation. The primary objective is to create a Virtual Private Cloud (VPC) with specific components, including two availability zones, public subnets, and EC2 instances with a focus on security, accessibility, and automation. The deployment aims to achieve a reliable and scalable architecture for hosting web applications while implementing best practices for network and security configurations. Additionally, it involves the installation of Jenkins for continuous integration and deployment, creating a robust foundation for future application development and maintenance. The documentation and Jenkins pipeline execution will provide a clear path for making changes to the deployed application while ensuring security and scalability, thereby enabling a streamlined development and deployment workflow.

## Building our own Infrastructure using Terraform

Terraform as Infrastructure as code manages and provisions infrastructure through code instead of through manual process. Prior to this deployment, we were configuring infrastructure resources through AWS Cloud UI.

In this Terraform-based infrastructure provisioning project, we've crafted a robust environment in Amazon Web Services to host our web application and streamline deployment processes. At the heart of this architecture is an Amazon Virtual Private Cloud (VPC) that provides network isolation and control. Within the VPC, we've established two Availability Zones (AZs) to enhance availability and fault tolerance. The VPC further contains two public subnets to house our Amazon Elastic Compute Cloud (EC2) instances. These EC2 instances play a pivotal role—our first instance serves as a Jenkins automation server, allowing for continuous integration and deployment, while the second hosts the application. To ensure secure access, we've employed a custom security group that regulates incoming and outgoing traffic for the instances on specified ports (8080, 8000, and 22). To route traffic appropriately, we've configured a dedicated route table. These resources collectively form a resilient and scalable infrastructure, empowering us to maintain and deploy our application with efficiency and security.


## Jenkins Installation/Configuration and SSH connection in first instance

**1: Install Jenkins**
- Followed the official Jenkins installation documentation 

**2: Create a Jenkins User and Log In**
- Created a Jenkins user account.
- Set up a password for the Jenkins user.

**Note**: 
- For detailed steps, refer to Deployment 3 documentation.
- `sudo -u jenkins -i` to switch user to Jenkins

**3: Generate SSH Keys**
-  Used the `ssh-keygen` command to generate a public and private SSH key pair.

**4: Copy SSH Public Key to Second Instance**
-  Copied the contents of the generated SSH public key.
-   Pasted the public key contents into the `authorized_keys` file on the second instance for SSH key-based authentication.
   
**5: Test SSH Connection**
- Tested the SSH connection between the two instances to ensure successful communication.

**6: Exit Jenkins User**
- Logged out of the Jenkins user account.

**7: Install Software in Ubuntu User**
- Logged in as the Ubuntu user.
- Installed the following software packages:
   - `software-properties-common`
   - `python3.7`
   - `python3.7-venv`

**Automation Scripts**:

- The `deploy_jenkins.sh` script was used to automate the Jenkins installation process.
- The `second_last.sh` script was used to automate the final step of software installation in the Ubuntu user account.

## Software configuration in second instance
Similar to software configuration in first instance following software packages were installed:
   - `software-properties-common`
   - `python3.7`
   - `python3.7-venv`
Similarly, `second_last.sh` script was used to automate the software installation process.

## Jenkinsfilev1 & Jenkinsfilev2 Integration:

In both Jenkinsfilev1 and Jenkinsfilev2, the following commands were employed to establish SSH connections to the second instance, facilitating the retrieval and execution of the necessary scripts at each step defined within the Jenkinsfile. This achievement represents a significant advancement in automating deployment and configuration tasks, leading to a more streamlined process for executing scripts on the secondary instance as part of the Jenkins pipeline.

**For Jenkinsfilev1:**

```shell
scp  /var/lib/jenkins/workspace/Deployment5_new_main/setup.sh ubuntu@34.238.52.125:/home/ubuntu
ssh ubuntu@34.238.52.125 'bash -s </home/ubuntu/setup.sh'
```

**For Jenkinsfilev2:**

```shell
scp setup2.sh ubuntu@34.238.52.125:/home/ubuntu
ssh ubuntu@34.238.52.125 'bash -s </home/ubuntu/setup2.sh'
```
```shell
scp  /var/lib/jenkins/workspace/Deployment5_new_main/pkill.sh ubuntu@34.238.52.125:/home/ubuntu
ssh ubuntu@34.238.52.125 'bash -s </home/ubuntu/pkill.sh'
```



## Initial Deployment using Jenkinsfilev1

Created a multi branch pipeline to run the Jenkinsfilev1 and deploy the Retail Banking application

**Result**: Succesfully deployed the flask application

![image](https://github.com/SaraGurungLABS01/Deployment_5/assets/140760966/7b3b287c-ebd2-4db7-8c29-dfac7c312226)

![image](https://github.com/SaraGurungLABS01/Deployment_5/assets/140760966/6be17070-4747-415d-b301-6b4dcde8a904)

## Modification to HTML File 

Made the following changes in the html file "home.html"

![image](https://github.com/SaraGurungLABS01/Deployment_5/assets/140760966/eb190222-8cac-44ce-b6fa-7e117eed8a37)

## Final Deployment using Jenkinsfilev2

Ran build again.

![image](https://github.com/SaraGurungLABS01/Deployment_5/assets/140760966/a0383bc1-b784-4808-8f5e-29d6877e0e96)


![image](https://github.com/SaraGurungLABS01/Deployment_5/assets/140760966/aa9266ef-e6e2-4dc9-a20a-a454e7789fbc)



















