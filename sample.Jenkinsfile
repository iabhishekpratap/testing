pipeline {
    agent any

    tools {
        maven "jenkins-maven"
    }

    stages {
        stage('checkout') {
            steps {
                git 'https://github.com/iabhishekpratap/simple-java-maven-app.git'
            }
        }

        stage("Build") {
            steps {
                sh 'mvn clean package'
            }
        }

        stage("Test") {
            steps {
                sh "mvn test"
            }
            post {
                always {
                    junit '**/target/surefire-reports/TEST-*.xml'
                }
            }
        }

        stage("Deploy") {
            steps {
                sh 'echo deployed'
            }
        }
    }

    post {
        success {
            script {
                emailext subject: "Jenkins Build SUCCESS - ${JOB_NAME} #${BUILD_NUMBER}",
                         body: "Good news! The build was successful.\nJob: ${JOB_NAME}\nBuild Number: ${BUILD_NUMBER}\nCheck console output: ${BUILD_URL}",
                         to: 'iapsingh@outlook.com',
                         recipientProviders: [[$class: 'DevelopersRecipientProvider']]
            }
        }

        failure {
            script {
                emailext subject: "Jenkins Build FAILURE - ${JOB_NAME} #${BUILD_NUMBER}",
                         body: "Unfortunately, the build has failed.\nJob: ${JOB_NAME}\nBuild Number: ${BUILD_NUMBER}\nCheck console output: ${BUILD_URL}",
                         to: 'iapsingh@outlook.com',
                         recipientProviders: [[$class: 'DevelopersRecipientProvider']]
            }
        }
    }
}
