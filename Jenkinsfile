def AUTHOR
def BUILD_TIME
pipeline {
    agent any

    environment {
        APP_VERSION = "1.0.0"
        ENVIRONMENT = "DEV"
        DEPLOY_ENABLED = "true"
    }

    stages {

        stage('Info') {
            steps {
                script {
                       AUTHOR = sh(
                            script: "git log -1 --pretty=format:'%an'",
                            returnStdout: true
                        ).trim()
                        echo "Autor: ${AUTHOR}"
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
                        echo "Deploying version ${env.APP_VERSION}"
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
                BUILD_TIME = currentBuild.durationString
                echo "Duration: ${currentBuild.durationString}"
                echo "DEBUG AUTHOR=${AUTHOR}"
                echo "DEBUG BUILD_TIME=${BUILD_TIME}"
            }

            echo """
            Build result: ${currentBuild.currentResult}
            Author: ${AUTHOR}
            Duration: ${BUILD_TIME}
            """
        }

        success {
            mail to: 'kamil.nierzwicki.ele@gmail.com',
                 subject: "SUCCESS: ${env.JOB_NAME}",
                 body: """
                 Deployment successful

                 Version: ${env.APP_VERSION}
                 Environment: ${env.ENVIRONMENT}
                 Author: ${AUTHOR}
                 Duration: ${BUILD_TIME}
                 """
        }

        failure {
            mail to: 'kamil.nierzwicki.ele@gmail.com',
                 subject: "FAILED: ${env.JOB_NAME}",
                 body: """
                 Pipeline failed

                 Job: ${env.JOB_NAME}
                 Author: ${AUTHOR}
                 Duration: ${BUILD_TIME}
                 """
        }
    }
}
