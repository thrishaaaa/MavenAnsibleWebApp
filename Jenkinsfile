pipeline {
    agent any

    tools {
        maven 'Maven' // Use the name configured in Jenkins Global Tool Configuration
    }

    environment {
        WAR_PATH = "${env.WORKSPACE}/target/MavenAnsibleWebApp.war"
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
                sh 'ls -l target/'
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/*.war', fingerprint: true
            }
        }

        stage('Deploy') {
            steps {
                sh """
                    echo "Deploying WAR: $WAR_PATH"
                    ansible-playbook ansible/playbook.yml \
                        -i ansible/hosts.ini \
                        --extra-vars "war_path=$WAR_PATH"
                """
            }
        }
    }
}
