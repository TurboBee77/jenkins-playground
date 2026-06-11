pipeline {

  agent any

  enviroment {
    APP_NAME = "jenkins-playground"
  }

  stages {

    stage('Hello') {

      steps {

        echo 'Hello from Jenkins'
      }
    }

    stage('Check Tools') {
      steps {
        sh 'git --version'
        sh 'python3 --version || python --version'
      }
    }

    stage('Workspace') {

      steps {

        sh 'pwd'
        sh 'ls -la'
      
      }
    }
  }

  post {

    success { 
      echo 'Pipeline completed successfully'
    }

    failure {
      echo 'Pipaline failed'
    }
  }
}
