pipeline {

    agent any

    options {
        timeout(time: 30, unit: 'MINUTES')
        retry(2)
    }

    environment {
        APP_NAME = "mywebsite"
        APP_BUILD_NUMBER = "${BUILD_NUMBER}"
    }

    stages {

        stage("Docker Confirmation")
        {
            steps{
                sh "docker --version"
                sh "cat /etc/os-release"
            }
        }

        stage("Build") {
            steps {
                echo "Build Using Docker Agent with Docker YML"
                sh"docker compose up -d"
                echo "Build using Docker Compose Completed"
            }
        }

        stage("Verify Container") {
            steps {
                sh"docker ps"
            }
        }

        
        stage("Debug Branch") {
            steps {
                echo "BRANCH_NAME = ${env.BRANCH_NAME}"
                echo "GIT_BRANCH = ${env.GIT_BRANCH}"
            }
        }

      
    }

    post {
        success {
            echo "${env.APP_NAME} deployment successfully"
        }
        failure {
            echo "${env.APP_NAME} deployment failed"
        }
        // always {
        
        //         cleanWs()
            
        // }
    }
}