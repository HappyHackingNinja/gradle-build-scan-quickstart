pipeline {
    agent {
        docker {
            image 'gradle:jdk8-alpine'
            args '-v /root/.m2:/root/.m2'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'gradle clean build'
            }
        }
        stage('Test') { 
            steps {
                sh 'gradle test' 
            }
            post {
                always {
                    publishHTML target: [
                        allowMissing: false,
                        alwaysLinkToLastBuild: false,
                        keepAll: true,
                        reportDir: 'build/reports/tests/test',
                        reportFiles: 'index.html',
                        reportName: 'Gradle Report'
                    ]
                }
            }
            
        }
    }
}
