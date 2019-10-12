pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'echo $PATH'
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