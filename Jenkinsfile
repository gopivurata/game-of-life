pipeline {
    agent { label 'NODE-1'}
    stages {
        stage('clone the repository of game of life') {
            agent { label 'NODE-1'}
            steps {
                git url: 'https://github.com/gopivurata/game-of-life.git', 
                    branch: 'master'
            }

        }
        stage('build the code of game of life') {
            tools {
                jdk 'JAVA-8'
            }
            steps {
                sh "mvn package"
            }
        }
    }
}
              
