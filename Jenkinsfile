pipeline {
  agent {
    kubernetes {
      yaml '''
        apiVersion: v1
        kind: Pod
        spec:
          containers:
          - name: maven
            image: maven:alpine
            command:
            - cat
            tty: true
        '''
    }
  }
  stages {
    stage('Run maven') {
      steps {
        container('maven') {
          sh 'mvn -version'
        }
      }
    }

    stage('Clean') {
      steps {
        container('maven') {
          sh '''
          echo "Cleaning environment"
          mvn clean
          '''

        }
      }
    }

    stage('Install') {
      steps {
        container('maven') {
          sh '''
          echo "Install application"
          mvn install
          '''
        }
      }
    }

    stage('Test') {
      steps {
        container('maven') {
          sh '''
          echo "Test application"
          mvn test
          '''
        }
      }
    }

    stage('Package') {
      steps {
        container('maven') {
          sh '''
          echo "Package application"
          mvn package
          ls -la
          ls -la /target
          '''
        }
      }
    }

    stage('Deploy') {
      steps {
        container('maven') {
          sh 'echo "Deploy to kubernetes"'
        }
      }
    }

  }
}
