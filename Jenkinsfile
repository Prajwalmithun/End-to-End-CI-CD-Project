pipeline {
    agent {
    docker 
    {
      image 'abhishekf5/maven-abhishek-docker-agent:v1'
      args '--user root -v /var/run/docker.sock:/var/run/docker.sock' // mount Docker socket to access the host's Docker daemon
    }
  }
    stages {
        stage('build') {
            steps {
                sh 'ls -ltrh'
                sh 'cd End-to-End-CI-CD-Project && mvn clean install'
            }
        }
    }
}