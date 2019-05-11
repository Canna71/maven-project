pipeline {
    agent any
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

        stage ('Deploy to staging') {
            steps {
                build job: 'Deploy to staging'
            }
        }

        
        stage ('Deploy to production') {
            steps {
                // will fail if no approved within 5 days
                timeout(time:5, unit:'DAYS') {
                    // can have a submitter argument
                    input message: 'Approve PRODUCTION Deplyment'
                }

                build job: 'deploy to prod'
            }

            post {
                success {
                    echo 'Code deployed to Production'
                }

                failure {
                    echo 'Deplyment failed.'
                }
            }
        }
    }
}