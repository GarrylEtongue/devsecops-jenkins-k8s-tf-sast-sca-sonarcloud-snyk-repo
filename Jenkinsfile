	pipeline {
    agent any
    tools { 
        maven 'Maven_3_2_5'
    }
    stages {
        stage('CompileandRunSonarAnalysis') {
            steps {	
                sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=amoneywebapp -Dsonar.organization=amoneywebapp -Dsonar.host.url=https://sonarcloud.io -Dsonar.token=e2419047b9ccae97286741265b800300a178a16b'
            }
        } 
        stage('RunSCAAnalysisUsingSnyk') {
            steps {		
                withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
                    sh 'mvn snyk:test -fn'
                }
            }
        }
    
    	stage('Build') { 
            steps { 
               withDockerRegistry([credentialsId: "dockerlogin", url: ""]) {
                 script{
                 app =  docker.build("asg")
                 }
               }
            }
    }

	stage('Push') {
            steps {
                script{
                    docker.withRegistry('https://145988340565.dkr.ecr.us-west-2.amazonaws.com', 'ecr:us-west-2:aws-credentials') {
                    app.push("latest")
                    }
                }
            }
    	}
    
    }
}
