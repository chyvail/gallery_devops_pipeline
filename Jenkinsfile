pipeline {
    agent any
        stages {
            stage('build'){
                steps {
                    echo 'Building our software'
                    sh 'npm install'
                }
            }
            stage('test'){
                steps {
                    echo 'test software'"
                    sh 'npm test'
                }
            }
            stage('deploy to Heroku'){
                steps {
                    withCredentials([usernameColonPassword(credentialsId: 'heroku', variable: 'HEROKU_CREDENTIALS' )]){
                    sh 'git push https://${HEROKU_CREDENTIALS}@git.heroku.com/gentle-temple-39284.git master'
                    }
                }
            }
        }
}