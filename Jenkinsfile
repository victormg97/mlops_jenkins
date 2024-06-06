pipeline {

    agent any

    stages {

        stage('Checkout') {

            steps {

                checkout scm

            }

        }

        stage('Install Dependencies') {

            steps {

                sh '''

                   sudo apt-get update

                   sudo apt-get install python3-venv

                '''

            }

        }

        stage('Setup Python Environment') {

            steps {

                sh '''

                   python3 -m venv venv

                   . venv/bin/activate

                   pip install --upgrade pip

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