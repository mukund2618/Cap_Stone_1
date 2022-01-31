pipeline {
  agent any
  stages {
    stage('Docker Build') {
      steps {
         sh 'docker build -t mukund2618/cap_stone_1:latest .'
      }
    }
    stage('Docker Push') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
          sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
          sh 'docker push mukund2618/cap_stone_1'
         }
      }
    }
    stage('My webapp Deployment with ansible playbook in Minikube Environment'){
      steps{
       withCredentials([usernamePassword(credentialsId: 'Live', passwordVariable: 'passwd_Live', usernameVariable: 'user_Live')]) {
	sh 'ansible-playbook ansible.yml'
}
       }
    }  
  }
}



