pipeline {
    agent any

    tools {
        maven 'Maven' // Make sure 'Maven' is configured in Jenkins Global Tool Configuration
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/imsudeeppatil/ansible.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.war', fingerprint: true
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                sh 'ansible-playbook ansible/playbook.yml -i ansible/hosts.ini'
            }
        }
    }
}
