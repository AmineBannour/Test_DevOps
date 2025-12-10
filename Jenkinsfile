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
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                echo 'Installation des dépendances Node.js'
                sh 'npm install'
            }
        }
        
        stage('Tests') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                echo 'Exécution des tests'
                sh 'npm test'
            }
        }
        
        stage('Build Docker') {
            steps {
                echo 'Construction de l\'image Docker'
                script {
                    sh 'docker build -t todo-app .'
                }
            }
        }
    }
}

