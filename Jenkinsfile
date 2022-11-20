pipeline {
    agent { label 'node'}
    stages {
        stage('clone the repository of game of life') {
            steps {
                git url: 'https://github.com/gopivurata/game-of-life.git', 
                    branch: 'master'
            }

        }
        stage('build the code of game of life') {
            tools {
                jdk 'java-8'
            }
            steps {
                sh "mvn package"
            }
        }
        stage('archive results') {
            steps {
                junit '**/surefire-reports/*.xml'
            }
        }
        stage('artifacts') {
            steps {
                archiveArtifacts artifacts: '**/target/*.war'
            }
        }
    }
}
              
              
