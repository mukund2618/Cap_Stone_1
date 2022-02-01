Hi this is my CI/CD declarative pipeline for rolling deployment.
DevOps Tools used in this projects are GIT, GIT HUB, Docker, Docker Hub, Jenkins, Ansible & Kubernetes.
Whole Infrastructure hosted in AWS Cloud Platform.
This project have two servers namely Jenkins & Live server all with base OS Ubuntu 20.04. 
Jenkins Server:
               EC2: t2.micro
               Base OS: Ubuntu 20.04
               RAM: 4 GB
               CPU: 1 core 2.4 Ghz
  Softwares Installed:
               GIT
               Docker
               Jenkins
               Ansible
Live Server:
            EC2: t2.medium
            Base OS: Ubuntu 20.04
            CPU: 2 Core 2.4 Ghz
            RAM: 4 GB
  Softwares Installed:
            Minikube
            Ansible
Steps followed in Jenkins Server:
  1. Create dockerfile which pulls apache2 image and copy my index.html to the default apache /usr/local/apache2/htdocs/.
  2. Create a repository in Github and clone it to local Machine.
  3. Login to Jenkins Server and create a declarative pipeline job and configure the below mentioned stages with steps.
        stage 1: GIT, GIT HUB Integration with Jenkins.
        stage 2: Build Docker image using dockerfile.
        stage 3: Push docker image to container registry Docker Hub.
        stage 4: Pull docker image.[This operation is done through K8s.yml]
        stage 5: Copy the necessary files from jenkins to live server.
        stage 5: Deploy app it to Minikube cluster installed in Live server by executing k8s.yml.
  steps followed in Live server:
  1. install docker and start it.
  2. install Minikube and start it to run with driver=none.
  3. Enable Minikube to start during boot.
  4. Execute the ansible.yml which inturn executes k8s.tml to deploy our webpage application.
  5. Application can be accessed with http://publicip:32000.
  
  we have now successfully deployed our webapp in CI/CD declarative pipeline using devops tools GIT, GIT HUB, Docker, Ansible & Kubernetes.
            
