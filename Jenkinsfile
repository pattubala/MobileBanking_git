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
			 // SONAR_SCANNER_OPTS = "-Xmx2g"
				scannerHome = tool "SonarQube_3.2"
      } 
      steps {
	withSonarQubeEnv('SonarQube_6.7.5') {
        // bat 'cd'
        bat '%scannerHome%/bin/sonar-scanner.bat -Dsonar.projectKey=MobileBanking_git -Dsonar.projectName=MobileBanking_git -Dsonar.projectVersion=1.0 -Dsonar.sources=src/ -Dsonar.sourceEncoding=UTF-8 -Dsonar.language=java -Dsonar.java.binaries=WebContent/WEB-INF/classes'	
      	}
      }
    }
	  stage('Nexus') {
		  steps {
		  	nexusPublisher nexusInstanceId: 'Nexus_3.12', nexusRepositoryId: 'MobileWeb_Ant', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: 'C:/Program Files (x86)/Jenkins/workspace/Pipeline-Sample/wars/mobilebanking_*.war']], mavenCoordinate: [artifactId: 'MobileBanking_git', groupId: 'com.ibm.services', packaging: 'war', version: '1.0']]]

		  }
	  
	  }
  }
}
