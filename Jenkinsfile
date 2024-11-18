pipeline {
    agent {
        label 'sonar'
    }
    environment {
        SCANNER_HOME=tool 'sonar-scanner'
    }
    stages {
        stage('git scm') {
            steps {
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'git-cred', url: 'https://github.com/chaiithu/bingo1.git']])
                }
           }
           stage ('sonarqube analysis') {
           steps{
                script{
                       withSonarQubeEnv('sonar-server') {
                        sh """$SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=sonar.4 \
                        -Dsonar.projectKey=sonar.4"""
                       }
                }
           }
           }
       stage ('quality gate') {
    steps {
          script {
               waitForQualityGate abortpipeline: false, credentialsid: 'sonar-token'
           }
      }
       }
    }
