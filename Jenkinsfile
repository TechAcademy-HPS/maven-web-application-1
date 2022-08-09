
def buildno = BUILD_NUMBER
pipeline {
    agent any
    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "maven3.6.3"
    }

    stages {
        stage('Build') {
            steps {
                git credentialsId: 'githubcredentials', url: 'https://github.com/TechAcademy-HPS/maven-web-application-1.git'
                 sh "mvn clean package"

            }
        }
        stage('build docker image') {
            steps {
		    sh "docker build -t yoshithadocker/ltiproject:${buildno} ."
                }

            }
  
           stage('deploy') {
            steps {
              ansiblePlaybook become: true, disableHostKeyChecking: true, installation: 'Ansible', inventory: 'hosts.inv', playbook: 'Deploy.yml'
                 }
            }
			
        }
}
