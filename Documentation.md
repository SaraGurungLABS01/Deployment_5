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


In the real world, businesses and developers frequently update web application interfaces to adapt to evolving user preferences, industry trends, or regulatory requirements. For instance, they may need to change the appearance, layout, or content of web pages to align with a rebranding effort or incorporate new functionalities.

These changes could be as simple as updating text, colors, or images, or as complex as adding interactive components and enhancing navigation. Furthermore, web applications may need to remain in sync with backend systems, databases, and third-party services, which often necessitates front-end modifications.

In our case, the HTML modification represents a scenario where, in response to user feedback or a strategic decision, we've improved a web page to enhance the user experience. In this context, our deployment process provides a structured and automated way to roll out these changes.

## Final Deployment using Jenkinsfilev2

Ran build again.

![image](https://github.com/SaraGurungLABS01/Deployment_5/assets/140760966/a0383bc1-b784-4808-8f5e-29d6877e0e96)


![image](https://github.com/SaraGurungLABS01/Deployment_5/assets/140760966/aa9266ef-e6e2-4dc9-a20a-a454e7789fbc)


The act of deploying the updated HTML file is a reflection of a real-world deployment process. In a production environment, deploying these types of changes is a crucial and routine task. It involves maintaining service availability and reliability while incorporating updates.

By demonstrating the second deployment, we showcase how infrastructure automation with Terraform and continuous integration with Jenkins significantly ease the process of updating a web application. This approach ensures minimal disruption to the application's availability and is essential for maintaining a seamless user experience.

In summary, the modifications to the HTML file in this second deployment exemplify the iterative and dynamic nature of web development and the importance of efficient, automated deployment processes in keeping web applications aligned with real-world business and user needs.

## Issues and Troubleshooting

During the deployment process, several issues were encountered. Some of them are:

**1. No Public Ip's for both of my instances** 

![image](https://github.com/SaraGurungLABS01/Deployment_5/assets/140760966/1859a351-f214-4949-a8bb-473dea26231a)

**Resolution:**
After including the following line of code in the Instance resource block:

```terraform
associate_public_ip_address = true  # Enable Auto-assign public IP
```

The successful implementation of the associate_public_ip_address attribute within the Instance resource block enabled the automatic assignment of public IP addresses to the user's EC2 instances. This resolution effectively addressed the initial problem of missing public IPs for the instances. Consequently, the instances now possess associated public IP addresses, facilitating internet connectivity.

**2. SSH Permission Denied**

The error indicated that Jenkins was unable to authenticate via SSH key when connecting to a remote server.

![image](https://github.com/SaraGurungLABS01/Deployment_5/assets/140760966/40d4d03e-4760-4e79-ba6e-a79f650a180d)
![image](https://github.com/SaraGurungLABS01/Deployment_5/assets/140760966/3304471f-8fc2-4c8f-9d9d-978ae73a5fd3)

**Resolution:**

Make sure to sign into the Jenkins user and test the ssh connection to the second instance. Prior to the resolution, SSH connection was established between the user (Ubuntu) and the second instance.

Use the below command to switch to jenkins user:

```bash
sudo -u jenkins -i
```







## Optimization

**Should you place both instances in the public subnet? Or should you place them in a private subnet? Explain why?**

In this deployment scenario, it's advisable to place the Jenkins server in a private subnet for enhanced security while accommodating the other application instance in a public subnet. This configuration provides a balance between security and accessibility. Placing the Jenkins server in a private subnet shields it from direct internet access, reducing potential security risks, and ensuring the sensitive Jenkins environment is protected. Simultaneously, the application instance in the public subnet can effectively interact with external resources and users, maintaining accessibility. This approach aligns with security best practices and creates a robust and secure foundation for our infrastructure.



























