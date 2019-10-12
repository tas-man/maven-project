pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                withMaven(
                // Maven installation declared in the Jenkins "Global Tool Configuration"
                maven: 'localMaven',
                // Maven settings.xml file defined with the Jenkins Config File Provider Plugin
                // We recommend to define Maven settings.xml globally at the folder level using 
                // navigating to the folder configuration in the section "Pipeline Maven Configuration / Override global Maven configuration"
                // or globally to the entire master navigating to  "Manage Jenkins / Global Tools Configuration"
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