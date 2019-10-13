pipeline {
    agent any
        parameters {
            string(name: 'tomcat_dev', defaultValue: '13.48.3.155', description: 'Staging Server')
            string(name: 'tomcat_prod', defaultValue: '13.53.171.154', description: 'Production Server')
        }
        triggers {
            pollSCM('* * * * *')
        }
    
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage('Deployment') {
            parallel {
                stage('Deploy to Staging') {
                    steps {
                        sh "scp -i /Users/Shared/Jenkins/.ssh/master-jenkins-demo.pem **/target/*.war ec2-user@${params.tomcat_dev}:/var/lib/tomcat7/webapps"
                    }
                }
                stage('Deploy to Production') {
                    steps {
                        sh "scp -i /Users/Shared/Jenkins/.ssh/master-jenkins-demo.pem **/target/*.war ec2-user@${params.tomcat_prod}:/var/lib/tomcat7/webapps"
                    }
                }
            }
        }
    }

}