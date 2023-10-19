pipeline {
    agent any

    tools {
        maven "M3"
    }

    stages {
        stage('prepare') {
            steps {
                scm checkout
            }
        }
        stage('Build') {
            steps {
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
            }

            post {
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
    }
}
