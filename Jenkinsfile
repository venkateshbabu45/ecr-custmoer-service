pipeline {
  agent any
  tools { 
        maven 'Maven'
        jdk 'JAVA_HOME'
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
        docker.build('address-service')
      }
    }
   
    stage('Push ECRImage') {
      steps {
        docker.withRegistry('https://990456062402.dkr.ecr.us-east-1.amazonaws.com', 'ecr:us-east-1:AKIAJ2TAT4FMKSHX3BTA') {
          docker.image('address-service').push('latest')
        }
      }
    }
  }
}
