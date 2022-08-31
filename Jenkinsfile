pipeline {
    agent any

    stages {

        stage('Get Source') {
            steps {
                git url: 'https://github.com/eudespaz/jenkins_prod.git', branch: 'master'
            }
        }
    
        stage('Docker Build') {
            steps {
                script {
                    dockerapp = docker.build("eudespaz/jenkins-producao-kurier:${env.BUILD_ID}",
                    '-f /var/jenkins_home/workspace/Projeto-JENKINS-PRODUCAO-KURIER/Dockerfile .')
                }
            }
        }
        
        stage('Docker Push Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                    dockerapp.push('latest')
                    dockerapp.push("${env.BUILD_ID}")

                    }
                }
            }       
        }
    }
}

