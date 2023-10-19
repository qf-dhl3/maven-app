pipeline {
    agent any

    tools {
        maven "M3"
    }

    stages {
        stage('prepare') {
            steps {
                checkout scm
            }
        }
        stage('scan') {
            steps {
                sh "mvn clean verify sonar:sonar \
                        -Dsonar.projectKey=mavenapp \
                        -Dsonar.projectName='mavenapp' \
                        -Dsonar.host.url=http://3.110.218.203:9000 \
                        -Dsonar.token=sqp_76cea8d0b336fa82219eef26681388ae1b033ab6"
            }
        }
        stage('Build') {
            steps {
                sh "mvn -Dmaven.test.failure.ignore=true -s settings.xml clean deploy"
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
