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
    }
}