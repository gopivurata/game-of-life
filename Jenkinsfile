pipeline {
    agent  { label 'NODE' }
    triggers { pollSCM('* * * * *') }
    stages {
        stage('git') {
            steps {
                git branch: 'my_branch', url: 'https://github.com/gopivurata/game-of-life.git'
            }

        }
        stage('build') {
            steps {
                sh '/usr/share/maven/mvn package'
            }
        }
        stage('archive results') {
            steps {
                junit '**/surefire-reports/*.xml'
            }
        }
        stage('artifacts') {
            steps {
                archiveArtifacts artifacts: '**/*.jar'
            }
        }
    }
}