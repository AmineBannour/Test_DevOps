pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                echo 'Récupération du code du dépôt Git'
                checkout scm
            }
        }
        
        stage('Install dépendances Node') {
            steps {
                echo 'Installation des dépendances Node.js'
                sh '''
                    docker run --rm -v "$PWD":/app -w /app node:18-alpine npm install
                '''
            }
        }
        
        stage('Tests') {
            steps {
                echo 'Exécution des tests'
                sh '''
                    docker run --rm -v "$PWD":/app -w /app node:18-alpine npm test
                '''
            }
        }
        
        stage('Build Docker') {
            steps {
                echo 'Construction de l\'image Docker'
                sh 'docker build -t todo-app .'
            }
        }
    }
}

