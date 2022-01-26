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
        withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
          sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
          sh 'docker push mukund2618/cap_stone_1'
         }
      }
    }
    stage('Connecting to stage machine') {
      steps {
          sshagent(['Stage']) {
             script{
                try{
                    sh "ssh ubuntu@34.219.164.48 docker pull mukund2618/cap_stone_1 && docker run -d -p 8585:80 mukund2618/cap_stone_1"
                }catch(error){
                    echo "========connectionf failed========"
                }
            }
        }
      }
    }
  }
}



