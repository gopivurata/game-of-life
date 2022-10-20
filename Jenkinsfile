pipeline {
    agent  { label 'NODE' }
    parameters {
        choice(name: 'BRANCH_TO_BUILD', choices: ['master', 'my_branch'], description: 'adedd branchess')
        string(name: 'MAVEN_GOAL', defaultValue: 'package', description: 'build package')
    }
    triggers {
        pollSCM('* * * * *')
    }
    stages {
        stage('git') {
            steps {
                git branch: "${params.BRANCH_TO_BUILD}", 
                url: 'https://github.com/gopivurata/game-of-life.git'
            }

        }
        stage('build') {
            steps {
                sh "/usr/share/maven/bin/mvn ${params.MAVEN_GOAL}"
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