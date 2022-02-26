pipeline {
  agent any
  stages {
    stage('Checkout SCM') {
      parallel {
        stage('Checkout SCM') {
          steps {
            git(url: 'https://github.com/Narendrakaduru/SaiJavaCode.git', branch: 'main', credentialsId: 'GitCred')
          }
        }

        stage('Check POM') {
          steps {
            fileExists 'pom.xml'
          }
        }

      }
    }

    stage('Build') {
      parallel {
        stage('Build') {
          steps {
            sh 'mvn clean package'
          }
        }

        stage('Print Tester') {
          steps {
            echo "The Tester is ${TESTER}"
          }
        }

        stage('Build No') {
          steps {
            echo "Print Build No ${BUILD_ID}"
          }
        }

      }
    }

    stage('Test') {
      steps {
        sh 'mvn test'
      }
    }

    stage('Deploy To Docker') {
      steps {
        sh 'docker build -t narendra8686/my-app:1.0.0 .'
      }
    }

  }
  environment {
    TESTER = 'NANI'
    BUILD_ID = '1.0.0'
  }
}