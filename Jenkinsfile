pipeline {

  agent any

  stages {

    stage('Hello') {

      steps {

        echo 'Hello from Jenkins'
      }
    }

    stage('Environment') {

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

    faliure {
      echo 'Pipaline failed'
    }
  }
}
