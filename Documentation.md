## Jenkins Installation/Configuration and SSH connection in first instance

**1: Install Jenkins**
1. Followed the official Jenkins installation documentation 

**2: Create a Jenkins User and Log In**
1. Created a Jenkins user account.
2. Set up a password for the Jenkins user.

**Note**: For detailed steps, refer to Deployment 3 documentation.

**3: Generate SSH Keys**
1. Used the `ssh-keygen` command to generate a public and private SSH key pair.

**4: Copy SSH Public Key to Second Instance**
1. Copied the contents of the generated SSH public key.
2. Pasted the public key contents into the `authorized_keys` file on the second instance for SSH key-based authentication.
   
**5: Test SSH Connection**
1. Tested the SSH connection between the two instances to ensure successful communication.

**6: Exit Jenkins User**
1. Logged out of the Jenkins user account.

**7: Install Software in Ubuntu User**
1. Logged in as the Ubuntu user.
2. Installed the following software packages:
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


