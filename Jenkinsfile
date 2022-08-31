pipeline {
    agent any

    stages {

        stage('Get Source') {
            steps {
                git url: 'https://github.com/eudespaz/dev-jenkins.git', branch: 'master'
            }
        }
    
        stage('Docker Build') {
            steps {
                script {
                    dockerapp = docker.build("vmtribunalimg:5000/jenkins-tribunal:${env.BUILD_ID}",
                    '-f /var/jenkins_home/workspace/DEV-JENKINS/Dockerfile .')
                }
            }
        }
        
        stage('Docker Push Image') {
            steps {
                script {
                    docker.withRegistry('https://vmtribunalimg:5000') {
                    dockerapp.push('latest')
                    dockerapp.push("${env.BUILD_ID}")

                    }
                }
            }       
        }
    }
}

