pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    echo "Contenu du code importé depuis git"
                    ls -la
                    echo "Versions des composants utilisés"
                    npm --version
                    node --version
                    echo "Début du build de l'application"
                    npm ci
                    npm run build
                    echo "Vérification du résultat"
                    ls -lart
                '''
            }
        }
        stage('Test') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    grep "index.htlm" build/
                    echo "Le fichier index.html existe bien"
                    echo "Lancement de la commande npm test"
                    npm test
                '''
            }            
        }
        stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }
    }
}
