pipeline {
    agent any

    stages {

        stage('System Update and Python Installation') {
            steps {
                sh '''
                    # Actualiza el sistema
                    sudo apt-get update -y
                    sudo apt-get upgrade -y
                    
                    # Instala Python3 y venv si no están instalados
                    if ! command -v python3 &> /dev/null; then
                        sudo apt-get install python3 -y
                    fi

                    if ! command -v python3-venv &> /dev/null; then
                        sudo apt-get install python3-venv -y
                    fi

                    if ! command -v pip3 &> /dev/null; then
                        sudo apt-get install python3-pip -y
                    fi
                '''
            }
        }

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Setup Python Environment') {
            steps {
                sh '''
                    # Crear el entorno virtual
                    python3 -m venv venv

                    # Activar el entorno virtual
                    . venv/bin/activate

                    # Actualizar pip
                    pip install --upgrade pip

                    # Instalar las dependencias
                    pip install pandas scikit-learn joblib
                '''
            }
        }

        stage('Train Model') {
            steps {
                sh '''
                    . venv/bin/activate
                    python train_model.py
                '''
            }
        }

        stage('Validate Model') {
            steps {
                sh '''
                    . venv/bin/activate
                    python validate_model.py
                '''
            }
        }

        stage('Deploy Model') {
            steps {
                sh '''
                    . venv/bin/activate
                    python deploy_model.py
                '''
            }
        }

    }
}
