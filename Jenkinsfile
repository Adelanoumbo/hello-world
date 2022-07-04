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
          sh 'echo "Cleaning environment"'
        }
      }
    }

    stage('Install') {
      steps {
        container('maven') {
          sh 'echo "Install application"'
        }
      }
    }

    stage('Test') {
      steps {
        container('maven') {
          sh 'echo "Test application"'
        }
      }
    }

    stage('Deploy') {
      steps {
        container('maven') {
          sh 'echo "Deploy to Harbor registry"'
        }
      }
    }

  }
}
