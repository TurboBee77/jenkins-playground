pipeline {
    agent any

    environment {
        APP_VERSION = "1.0.0"
        ENVIRONMENT = "DEV"
        DEPLOY_ENABLED = "true"

        AUTHOR = ""
        BUILD_TIME = ""
    }

    stages {

        stage('Info') {
            steps {
                script {
                       env.AUTHOR = sh(
                            script: "git log -1 --pretty=format:'%an'",
                            returnStdout: true
                        ).trim()
                        echo "Autor: ${env.AUTHOR}"
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    try {
                        echo "Building application..."
                        sh "echo Build OK"

                    } catch (Exception e) {
                        currentBuild.result = 'FAILURE'
                        error("Build failed")
                    }
                }
            }
        }

        stage('Test') {
          
            steps {
                script {
                    try {
                        echo "Running tests..."
                        sh "echo Tests OK"

                    } catch (Exception e) {
                        currentBuild.result = 'FAILURE'
                        error("Tests failed")
                    }
                }
            }
        }

        stage('Deploy') {

            when {
                expression {
                    env.DEPLOY_ENABLED == "true"
                }
            }

            steps {
                script {
                    try {
                        echo "Deploying version ${APP_VERSION}"
                        sh "echo Deployment OK"

                    } catch (Exception e) {
                        currentBuild.result = 'FAILURE'
                        error("Deploy failed")
                    }
                }
            }
        }
    }

    post {

        always {
            script {
                env.BUILD_TIME = currentBuild.durationString
            }

            echo """
            Build result: ${currentBuild.currentResult}
            Author: ${env.AUTHOR}
            Duration: ${env.BUILD_TIME}
            """
        }

        success {
            mail to: 'kamil.nierzwicki.ele@gmail.com',
                 subject: "SUCCESS: ${env.JOB_NAME}",
                 body: """
                 Deployment successful

                 Version: ${env.APP_VERSION}
                 Environment: ${env.ENVIRONMENT}
                 Author: ${env.AUTHOR}
                 Duration: ${env.BUILD_TIME}
                 """
        }

        failure {
            mail to: 'kamil.nierzwicki.ele@gmail.com',
                 subject: "FAILED: ${env.JOB_NAME}",
                 body: """
                 Pipeline failed

                 Job: ${env.JOB_NAME}
                 Author: ${env.AUTHOR}
                 Duration: ${env.BUILD_TIME}
                 """
        }
    }
}
