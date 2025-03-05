pipeline {
    agent any

    environment {
        GIT_REPO = 'https://github.com/prasannac-ai/test.git'
        BRANCH = 'main'
    }

    stages {
        stage('Pull Code') {
            steps {
                script {
                    checkout([$class: 'GitSCM', 
                        branches: [[name: '*/main']], 
                        userRemoteConfigs: [[url: 'https://github.com/prasannac-ai/test.git']]
                    ])
            }
        }

        stage('Build Application') {
            steps {
                script {
                    sh 'mvn clean package'
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    sh 'mvn test'
                }
            }
        }

        stage('Deploy with Ansible') {
            steps {
                script {
                    sh 'ansible-playbook -i hosts deploy.yml'
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check logs for details.'
        }
        always {
            echo 'Pipeline execution completed.'
        }
    }
}
