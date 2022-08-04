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
        /*stage('sonar') {
            steps {
                withSonarQubeEnv('SonarQube') {
                sh "mvn sonar:sonar"
                }

            }

           }*/
           stage('deploy') {
            steps {
                ansiblePlaybook credentialsId: 'tomcatec2credentials', disableHostKeyChecking: true, installation: 'ansible', inventory: 'hosts', playbook: 'deploy.yml'
                 }
            }
        }
}
