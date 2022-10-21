pipeline {
    agent  { label 'NODE' }
     tools {
                jdk 'JAVA-8'
            }
    parameters {
        choice(name: 'BRANCH_TO_BUILD', choices: ['master', 'my_branch'], description: 'adedd branchess')
        string(name: 'build', defaultValue: 'package', description: 'code build') }
    stages {
        stage('git') {
            steps {
                git branch: "${params.BRANCH_TO_BUILD}", 
                url: 'https://github.com/gopivurata/game-of-life.git'
            }

        }
        stage('build') {
            steps {
                sh "mvn ${params.build}"
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