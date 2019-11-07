pipeline {
  environment {
    registry = "auasad/expresscart"
    registryCredential = 'dockerhub'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        checkout scm
        git 'https://github.com/auasad/expressCart.git'
      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }
    stage('Stopping & remove Old Image'){
      steps{
        sshagent(['DockerDevServer']) {
          sh 'ssh -o StrictHostKeyChecking=no asad@10.128.0.3 docker stop expresscart-app || true'
          sh 'ssh -o StrictHostKeyChecking=no asad@10.128.0.3 docker rm expresscart-app || true'
        }  
      }
   }
    stage('Deploy Container on Dev') {
      steps{
      script {
        docker.withRegistry( '', registryCredential ) {
          def dockerRun = 'docker run -p 8080:1111 -d --name expresscart-app --link expressdb:expressdb auasad/expresscart:${BUILD_NUMBER}'
            sshagent(['instance-uat']) {
              sh "ssh -o StrictHostKeyChecking=no asad@10.128.0.3 ${dockerRun}"
           } }
        }
      }
    }
    stage("Successful"){
      steps{
        script {
          sh "echo CICD Done."
        }
      }    
    }
  }
}
