pipeline {
    agent any
    stages {
        stage('Initialize') {
            steps {
                echo '$PATH'
                sh 'echo $PATH'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn -version'
                sh 'mvn clean package'    
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
    }
}