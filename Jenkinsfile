pipeline {
  agent any
  tools { 
        maven 'Maven_3_2_5'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=amoneywebapp -Dsonar.organization=amoneywebapp -Dsonar.host.url=https://sonarcloud.io -Dsonar.token=e2419047b9ccae97286741265b800300a178a16b'
			}
        } 
  }
}
