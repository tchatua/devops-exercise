# Jenkins CI/CD Tool Configuration

## Commands to get the Jenkins admin password via command line
```sh
chmod 400 <keypair>
ssh -i <keypair> ec2-user@<public_dns>

sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```
# Copy the private key content attached to my docker host server 
```css
$ cat dockerHost-ec2/ohio_pem_key_pair.pem
```

## Install Require plugins on Jenkins
- Go to > `Manage Jenkins` > `Manage Jenkins`  > `Available plugins`
- Search and install:
    - Git 
    - GitHub 
    - ssh
    - ssh agent

<!-- ## Create a dedicated dockeradmin user on my dockerhost server
- add dockeradmin user in the sudoer file
- add dockeradmin user in the docker group
- On my dockerhost server:
    - Create a `dockeradmin` user and add it in the docker group
        - sudo useradd dockeradmin
        - sudo passwd dockeradmin
        - sudo visudo `dockeradmin  ALL=(ALL)       ALL`
        - sudo cat /etc/group | grep docker
        - id dockeradmin
        - sudo usermod -aG docker dockeradmin
        - sudo cat /etc/group | grep docker
- use dockeradmin user to generate his ssh key for the future authentication
```sh -->
<!-- su dockeradmin

id
uid=1001(dockeradmin) gid=1001(dockeradmin) groups=1001(dockeradmin),992(docker)

ssh-keygen -->
<!-- ``` -->

## Add a dockerhost credential on my Jenkins server
- **Manage Jenkins** > **Credentials** > **System** > **Global credentials (Unrestricted)** > **Add credentials**:
    - Kind: SSH Username with private key
    - ID: 172.31.30.95 (Private IP address of docker host server)
    - Description: Dockerhost server credential
    - Username: ec2-user
    - At `Private key` > SELECT `Enter directly` > `Add` > Copy and past the private key


## Configure the Jenkins system to ssh to my target remote dockerhost 
- **Manage Jenkins** > **System** > at `SSH remote hosts` SELECT **Add**:
    - Hostname?: 172.31.30.95 (Private IP address of docker host server)
    - port?: 22
    - Credentials: SELECT `user that will be use on my target EC2` **ec2-user** in this case
    - `Check connection` > make it is successful and save

<!-- ## To login into my docker host with ssh
```sh
ssh -i ohio_pem_key_pair.pem dockeradmin@18.191.242.47
ssh -i ohio_pem_key_pair.pem dockeradmin@3.128.189.18
``` -->

## Create Access Token on my DockerHub account
- It will be use in my Jenkinsfile as environment variable: DOCKERHUB_CREDENTIALS
- `Account Name` > `Account Settings` > `Security` > `New Access Token`
    - `Access token description`: jenkins
    - `Access permissions`: Read, Write, Delete
- `Generate` > Copy and save 
- **Add this credential to my Jenkins Server**
  - `Manage Jenkins` > `Credentials` > `Jenkins` > `Global credentials (unsrestricted)` >
  - `Add credentials`:
      - Kind: Username with password
      - Username: tchatua
      -  Password: `paste the token`
      -  ID: docker-hub-tchatua (Will be updated in my Jenkinsfile)
      -  Description: docker-hub-tchatua
      -  `Apply` and `Save`

## Create my jenkins job
