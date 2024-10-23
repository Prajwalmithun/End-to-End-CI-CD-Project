pipeline {
    agent {
    docker 
    {
      image 'maven:3.8.3-openjdk-17'
      // args '--user root -v /var/run/docker.sock:/var/run/docker.sock' // mount Docker socket to access the host's Docker daemon
    }
  }
    stages {
        stage('build') {
            steps {
                // sh 'ls -ltrh'
                sh 'mvn clean install'
            }
        }

         stage('Static Code Analysis') {
            environment {
                SONAR_URL = "http://13.56.140.138:9000/"
              }
            steps {
              withCredentials([string(credentialsId: 'sonarqube', variable: 'SONAR_AUTH_TOKEN')]) {
                sh 'mvn sonar:sonar -Dsonar.login=$SONAR_AUTH_TOKEN --Dsonar.host.url=${SONAR_URL}'
                echo 'SonarQube Static Code Analysis Completed'
              }
            }
        }
    }
}