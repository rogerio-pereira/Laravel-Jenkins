pipeline {
    agent any
    stages {
        stage("Verify tooling") {
            steps {
                sh '''
                    docker info
                    docker version
                    docker compose version
                '''
            }
        }
        stage("Clean all docker container") {
            steps {
                script {
                    try {
                        sh 'docker rm -f $(docker ps -a -q)'
                    }
                    catch(Exception e) {
                        echo "No running containers to clear up..."
                    }
                }
            }
        }
        stage("Start docker") {
            steps {
                sh 'make up'
                sh 'docker compose ps'
            }
        }
        stage("Run composer install") {
            steps {
                sh 'docker-compose run app composer install'
            }
        }
        stage("Run composer install") {
            steps {
                sh 'docker-compose run app php artisan test'
            }
        }
    }
    post {
        always {
            sh 'docker-compose down --remove orphans -v'
            sh 'docker-compose ps'
        }
    }
}