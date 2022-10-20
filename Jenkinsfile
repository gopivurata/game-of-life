pipeline {
    agent  { label 'NODE' }
    triggers { pollSCM('* * * * *') }
    parameters {
        choice(name: 'BRANCH_TO_BUILD', choices: ['master', 'my_branch'], description: 'Branch to build')
        string(name: 'MAVEN_GOAL', defaultValue: 'package', description: 'maven goal')

    }
    stages {
        stage('git') {
            steps {
                git branch: "${params.BRANCH_TO_BUILD}", url: 'https://github.com/gopivurata/game-of-life.git'
            }

        }
        stage('build') {
            steps {
                sh "mvn ${params.MAVEN_GOAL}"
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