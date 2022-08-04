pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "maven"
    }

    stages {
        stage('Build') {
            steps {
                git credentialsId: 'SSHKey', url: 'https://github.com/TechAcademy-HPS/maven-web-application.git'

                sh "mvn clean package"

            }
        }
        stage('sonar') {
            steps {
                withSonarQubeEnv('SonarQube') {
                sh "mvn sonar:sonar"
                }

            }

           }
           stage('deploy') {
            steps {
                sshagent(['tomcatcredentials']) {
                  sh "scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/javawebapp/target/maven-web-application.war ec2-user@13.126.141.194:/opt/apache-tomcat-9.0.65/webapps"
                 }
            }
        }
        }
}
