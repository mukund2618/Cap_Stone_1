pipeline {
  agent any
  stages {
    stage('Docker Build') {
      steps {
         sh 'docker build -t mukund2618/cap_stone_1 .'
      }
    }
    stage('Docker Push') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'DockerHub', passwordVariable: 'dockerpass', usernameVariable: 'Dockeruser')]) {
          sh "docker login -u ${env.Dockeruser} -p ${env.dockerpass}"
          sh 'docker push mukund2618/cap_stone_1'
         }
      }
    }
    stage('My webapp Deployment with ansible playbook in Minikube Environment'){
      steps{
        ansiblePlaybook credentialsId: 'Jenkins-Public', disableHostKeyChecking: true, installation: 'Ansible1', inventory: 'host.inv', playbook: 'ansible.yml'
     }
    }  
  }
}



