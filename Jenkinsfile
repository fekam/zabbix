pipeline {
    agent any

    environment {
        // Définir des variables d'environnement si nécessaire
        ANSIBLE_DIR = '/ansible'
    }

    stages {
        stage('Setup') {
            steps {
                echo "Navigating to ${ANSIBLE_DIR}"
                dir("${ANSIBLE_DIR}") {
                    echo 'Installing required roles using ansible-galaxy...'
                    sh 'ansible-galaxy install -r requirements.yml'
                }
            }
        }

        stage('Deploy Zabbix Server') {
            steps {
                dir("${ANSIBLE_DIR}") {
                    echo 'Running the Zabbix Server playbook...'
                    sh 'ansible-playbook -i hosts zabbix-server.yml'
                }
            }
        }
    }

    post {
        success {
            echo 'Zabbix Server installation completed successfully!'
        }
        failure {
            echo 'Zabbix Server installation failed.'
        }
    }
}
