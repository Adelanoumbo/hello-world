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
          rm -rf webapp/target/webapp.war || true
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
