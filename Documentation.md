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

For Jenkinsfilev1:

```shell
scp  /var/lib/jenkins/workspace/Deployment5_new_main/setup.sh ubuntu@34.238.52.125:/home/ubuntu
ssh ubuntu@34.238.52.125 'bash -s </home/ubuntu/setup.sh'
```

For Jenkinsfilev2:

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



















