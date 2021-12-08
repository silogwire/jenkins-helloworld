node {
 environment {
                 SONARQUBE_URL = "http://79.137.37.35"
                 SONARQUBE_PORT = "9000"
                 SONARQUBE_LOGIN = "7feb11a80127b3e132ef98b518d67e4115959d1a"
         }

	stage('Clone') {
		git 'https://github.com/silogwire/jenkins-helloworld.git'
	}
	stage('Build') {
		sh label: '', script: 'javac Main.java'
	}
	stage('Run') {
		sh label: '', script: 'java Main'
	}
	        stage('Sonarqube') {
    environment {
        scannerHome = tool 'SonarQubeScanner'
    }
    steps {
        withSonarQubeEnv('sonarqube') {
                      sh 'mvn sonar:sonar -Dsonar.projectKey=sonarqube_sonarqube_Hello  \
                                            -Dsonar.host.url=$SONARQUBE_URL:$SONARQUBE_PORT \
                                            -Dsonar.login=$SONARQUBE_LOGIN'

        }
//        timeout(time: 10, unit: 'MINUTES') {
//            waitForQualityGate abortPipeline: true
//        }
    }
}
        stage("Quality Gate") {
  steps {
    timeout(time: 1, unit: 'MINUTES') {
        waitForQualityGate abortPipeline: true
    }
  }
}

}
