pipeline {
    agent {
    docker 
    {
      // image 'maven:3.8.3-openjdk-17'
      // image 'prajwal3498/docker-agent-cicd:latest'
      image 'prajwal3498/docker-agent-cicd-amd64:latest'
      args '--user root -v /var/run/docker.sock:/var/run/docker.sock' // mount Docker socket to access the host's Docker daemon (we need in docker build and push step)
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
                SONAR_URL = "http://54.219.140.80:9000/"
              }
            steps {
              withCredentials([string(credentialsId: 'sonarqube', variable: 'SONAR_AUTH_TOKEN')]) {
                sh 'mvn sonar:sonar -Dsonar.login=$SONAR_AUTH_TOKEN -Dsonar.host.url=${SONAR_URL}'
                echo 'SonarQube Static Code Analysis Completed'
              }
            }
        }

        stage('Build and Push Docker Image') {
            environment {
                DOCKER_IMAGE = "prajwal3498/cicd-v1:${BUILD_NUMBER}"
                // DOCKERFILE_LOCATION = "java-maven-sonar-argocd-helm-k8s/spring-boot-app/Dockerfile"
                REGISTRY_CREDENTIALS = credentials('docker-cred')
              }

            steps {
              script {
                sh 'docker build -t ${DOCKER_IMAGE} .'
                def dockerImage = docker.image("${DOCKER_IMAGE}")
                docker.withRegistry('https://index.docker.io/v1/', "docker-cred") 
                {
                  dockerImage.push() 
                }
              }
            }
        }

    }

} 
        
      



    