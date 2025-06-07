pipeline {
    agent any
    
    tools {
        maven 'maven'  // Ensure this matches the name configured in Jenkins
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/thrishaaaa/MavenAnsibleWebApp.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/*.war', fingerprint: true
            }
        }

        stage('Deploy') {
            steps {
                sh 'mvn clean package'
                sh 'ansible-playbook ansible/playbook.yml -i ansible/hosts.ini'
            }
        }
    }
}
