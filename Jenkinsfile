pipeline {
    agent any
    tools {
        nodejs 'Node-19.1.0'
        }
        stages {
            stage('Clone the repo'){
                steps {
                    git 'https://github.com/jonnygovish/gallery.git'
                }
            }
            stage('build'){
                steps {
                    echo 'building'
                    sh 'npm install'
                }
            }
            stage('deploy to Heroku'){
                steps {
                    sh 'git push https://joshuachivile:7a90b5a2-d4d9-4daf-abc5-e7f2853d3f9c@git.heroku.com/gentle-temple-39284.git -f master'
                }
            }
        }
}