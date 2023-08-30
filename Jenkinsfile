pipeline {
    agent any
    stages {
        // stage("Verify tooling") {
        //     steps {
        //         sh '''
        //             docker info
        //             docker version
        //             docker-compose version
        //         '''
        //     }
        // }
        // stage("Clean all docker container") {
        //     steps {
        //         script {
        //             try {
        //                 /*
        //                  * Remove all containers that start with test.jenkins
        //                  *      Those are defined in docker-compose.yml > container_name
        //                  */
        //                 sh 'docker rm -f $(docker ps | grep test.jenkins. | cut -d ' ' -f1)'
        //             }
        //             catch(Exception e) {
        //                 echo "No running containers to clear up..."
        //             }
        //         }
        //     }
        // }
        // stage("Start docker") {
        //     steps {
        //         sh 'docker-compose up -d'
        //         sh 'docker compose ps'
        //     }
        // }
        stage("Run composer install") {
            steps {
                sh 'docker-compose run app composer install'
            }
        }
        stage("Run tests") {
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