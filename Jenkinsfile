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
        sh 'pwd'              // Prints the current directory where Maven runs
        sh 'ls -l target/'    // Lists files in the target directory (where WAR should be)
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
