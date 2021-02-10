pipeline {
    agent any


  stages {

     stage("Initial cleanup") {
          steps {
            dir("${WORKSPACE}") {
              deleteDir()
            }
          }
        }
  
    stage('Checkout SCM') {
      steps {
            git branch: 'main', url: 'https://github.com/darey-devops/php-todo.git'
      }
    }
    
 
      stage('Execute Unit Tests') {
      steps {
             sh './vendor/bin/phpunit'
      } 
      }
      
         stage('Code Analysis') {
      steps {
            sh 'phploc app/ --log-csv build/logs/phploc.csv'

      }
    }
    stage('SonarQube Quality Gate') {
        environment {
            scannerHome = tool 'SonarQubeScanner'
        }
        steps {
            withSonarQubeEnv('sonarqube') {
                sh "${scannerHome}/bin/sonar-scanner"
            }

        }
    }
      
}
}
