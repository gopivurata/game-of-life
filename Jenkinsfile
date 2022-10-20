pipeline {
    agent  { label 'NODE' }
    triggers { pollSCM('* * * * *') }
    parameters {
        choice(name: 'BRANCH_TO_BUILD', choices: ['master', 'my_branch'], description: 'Branch to build')

    }
    stages {
        stage('git') {
            steps {
                git branch: "${params.BRANCH_TO_BUILD}", url: 'https://github.com/gopivurata/game-of-life.git'
            }

        }
        stage('build') {
            steps {
                sh '/usr/share/maven/bin/mvn package'
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