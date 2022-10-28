pipeline {
    agent any
    
    stages {
        stage("git clone") {
            steps {
                git branch: 'main', url: 'https://github.com/bsekharreddy/simplecalc.git'
            }
        }
        stage('Cmake Build') {
        steps {
            sh 'cd /var/lib/jenkins/workspace/simplecalc'
            sh 'pwd'
            sh 'sudo -s cmake .'
            sh 'sudo -s make'
            sh 'sudo ./simplecalc'
            echo "CMake Build Success"
        }
    }
    stage('SonarQube analysis') {
     //tools {
        SonarQube 'sonarqube 4.7'
      }//
      steps {
        //withSonarQubeEnv('SonarQube') {
          sh "${scannerHome}/bin/sonar-scanner"
		  sh "sonar-scanner"//
		  echo "Analysis is Pending"
        }
      }
        
    }
}
}

