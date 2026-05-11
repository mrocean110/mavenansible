pipeline {
    agent any
    environment {
    LANG = 'en_US.UTF-8'
    LC_ALL = 'en_US.UTF-8'
    }
    tools {
        maven 'Maven'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/mrocean110/mavenansible.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'  
            }
        }
        stage('Archive'){
        steps{
        archiveArtifacts artifacts: 'target/test2.war', fingerprint:true
        }
        }

        stage('Deploy') {
            steps {
                sh 'mvn clean package'  
                sh 'ansible-playbook playbook.yml -i host.ini'
            }
        }       
    }

    post {
        success {
            echo 'Build and deployment successful!'
        }
        failure {
            echo 'Build failed!'
        }
    }

}
