pipeline {
    agent any

    environment {
        GITHUB_REPO = 'https://github.com/srivastava-basu/upgrad-capstone-project.git'       
    }

    stages {
        stage('Checkout') {
            steps {
                // Pull the latest code from GitHub
                git url: "${GITHUB_REPO}", branch: 'main'
            }
        }
        stage('Deploy to AWS') {
            steps {
                script {
                    // Copy index-aws.html to the Jenkins server and then run the playbook
                    sh """
                    cd /var/lib/jenkins/workspace/capsprj-nginx-deploy-pipeline/indexFiles
                    cp index-aws.html /home/ubuntu/indexFiles/index-aws.html
                    cd /var/lib/jenkins/workspace/capsprj-nginx-deploy-pipeline/ansibleWork
                    ansible-playbook playbook.yaml -i inventory
                    """
                }
            }
        }
        stage('Deploy to Azure') {
            steps {
                script {
                    // Copy index-aws.html to the Jenkins server and then run the playbook
                    sh """
                    cd /var/lib/jenkins/workspace/capsprj-nginx-deploy-pipeline/indexFiles
                    cp index-azure.html /home/ubuntu/indexFiles/index-azure.html
                    cd /var/lib/jenkins/workspace/capsprj-nginx-deploy-pipeline/ansibleWork
                    ansible-playbook playbook.yaml -i inventory
                    """
                }
            }
        }
    }
}
