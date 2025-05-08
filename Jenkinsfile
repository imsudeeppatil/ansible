pipeline {
    agent any  // Use any available agent
    
    environment {
        LANG = 'en_US.UTF-8'
        LC_ALL = 'en_US.UTF-8'
    }

    tools {
        maven 'Maven'  // Ensure this matches the Maven name configured in Jenkins Global Tools
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/imsudeeppatil/ansible.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'  // Run Maven build
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/*.war', fingerprint: true
            }
        }

        stage('Deploy') {
            steps {
                // Re-running build here is redundant if already built above
                // You may remove the following line if not needed
                // sh 'mvn clean package'
                
                sh 'ansible-playbook ansible/playbook.yml -i ansible/hosts.ini'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed. Check the logs for details.'
        }
    }
}
