pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    stage("build"){
      steps {
        bat 'ant all'
      }
    }
    stage('SonarQube analysis') {
			environment {
			  SONAR_SCANNER_OPTS = "-Xmx2g"
				scannerHome = tool "SonarQube_3.2"
      } 
      steps {
        bat 'cd'
        bat '%scannerHome%/bin/sonar-scanner.bat -D sonar-scanner.properties'
      }
	  }
  }
}
