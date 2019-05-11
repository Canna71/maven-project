pipeline {
    agent any

    parameters {
        string(name: "tomcat_dev", defaultValue: '34.251.0.180', description: 'Staging env')
        string(name: "tomcat_prod", defaultValue: '63.35.237.65', description: 'Prod env')

    }

    triggers {
        pollSCM('* * * * *') // not a realistic example
    }

    stage ('Deployments') {
        parallel {
            stage ('Deploy to Staging') {
                steps {
                    sh "scp -i /var/lib/docker/volumes/jenkins_home/_data/asw.pem **/target/*.war ec2-user@{params.tomcat_dev}:/var/lib/tomcat7/webapps"
                }
            }

            stage ('Deploy to Production') {
                steps {
                    sh "scp -i /var/lib/docker/volumes/jenkins_home/_data/asw.pem **/target/*.war ec2-user@{params.tomcat_prod}:/var/lib/tomcat7/webapps"
                }
            }
        }
    }
}