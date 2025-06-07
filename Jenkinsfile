pipeline {
    agent any
    
    tools {
        maven 'maven'  // Ensure this matches the Maven tool name in Jenkins config
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
                sh 'ls -l target/'  // Check WAR is created
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/*.war', fingerprint: true
            }
        }
        
        stage('Deploy') {
            steps {
                // Run ansible playbook assuming ansible-playbook is installed and configured
                sh 'ansible-playbook ansible/playbook.yml -i ansible/hosts.ini'
            }
        }
    }
}
