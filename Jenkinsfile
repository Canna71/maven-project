pipeline {
    agent any

    // parameters {
    //     string(name: "tomcat_dev", defaultValue: '34.251.0.180', description: 'Staging env')
    //     string(name: "tomcat_prod", defaultValue: '63.35.237.65', description: 'Prod env')

    // }

    // triggers {
    //     pollSCM('* * * * *') // not a realistic example
    // }

    stages {

        stage ('Build') {
            steps {
                sh 'mvn clean package'
                sh "docker build -f Staging/Dockerfile -t tomcat-8090:${env.BUILD_ID}"
            }

            post {
                success {
                    echo "Now Archiving..."
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        // stage ('Deployments') {
        //     parallel {
        //         stage ('Deploy to Staging') {
        //             steps {
        //                 sh "scp -i /var/jenkins_home/asw.pem **/target/*.war ec2-user@${params.tomcat_dev}:/var/lib/tomcat7/webapps"
        //             }
        //         }

        //         stage ('Deploy to Production') {
        //             steps {
        //                 sh "scp -i /var/jenkins_home/asw.pem **/target/*.war ec2-user@${params.tomcat_prod}:/var/lib/tomcat7/webapps"
        //             }
        //         }
        //     }
        // }
    }
}