pipeline {
  agent any
  tools { 
        maven 'Maven'
        jdk 'Java'
  }
  stages {
    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace... */
      steps {
        checkout scm
      }
    }
    stage('Build') {
      steps {
        sh 'mvn -B -DskipTests clean package'
        sh 'echo $USER'
        sh 'echo whoami'
      }
    }
    stage('Docker Build') {
      steps {
        sh '/usr/bin/docker build -t address-service .'
      }
    }
   
    stage('push image to ECR'){
      steps {
       withDockerRegistry(credentialsId: '60197c61-99a4-420f-b15c-90522e9ea7ad', url: 'http://508607970941.dkr.ecr.us-east-1.amazonaws.com/address-service') {
          sh 'docker tag address-service:latest 508607970941.dkr.ecr.us-east-1.amazonaws.com/address-service:latest'
          sh 'docker push 508607970941.dkr.ecr.us-east-1.amazonaws.com/address-service:latest'
        } 
      }
    }
   
  }
}
