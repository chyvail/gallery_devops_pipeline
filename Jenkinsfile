pipeline {
    agent any
    tools {
        nodejs 'Node-19.1.0'
        }
        stages {
            stage('Clone the repo'){
                steps {
                    git 'https://github.com/chyvail/gallery_devops_pipeline.git'
                }
            }
            stage('build'){
                steps {
                    echo 'building'
                    sh 'npm install'
                }
            }
            
            stage('test'){
                steps {
                    echo 'testing'
                    echo 'npm test'
                }
            }
            
            stage('deploy to Heroku'){
                steps {
                    withCredentials([usernameColonPassword(credentialsId: 'heroku', variable: 'HEROKU_CREDENTIALS' )]){
                        sh 'git push https://${HEROKU_CREDENTIALS}@git.heroku.com/gentle-temple-39284.git -f master'
    }
                }
            }
            
        }
        post {
                always {
                    script {
                        if (currentBuild.currentResult == 'FAILURE' || currentBuild.currentResult == 'SUCCESS'  ) {
                            step([$class: 'Mailer', notifyEveryUnstableBuild: true, recipients: "joshuachivile@gmail.com", sendToIndividuals: true])
                        }
                    }
                }
                success {
                    slackSend channel: '#joshua_ip1',
                        color: 'good',
                        message: "The pipeline ${currentBuild.fullDisplayName} completed successfully. Visit https://gentle-temple-39284.herokuapp.com/"
                }
                failure {
                    slackSend channel: '#joshua_ip1',
                            color: 'danger',
                            message: "The pipeline ${currentBuild.fullDisplayName} completed successfully."
                }
            }

}