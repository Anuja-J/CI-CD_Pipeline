pipeline {
    agent any
    tools {
        jdk 'jdk17'
        maven 'maven3' 
        nodejs 'node12'
        
    }
    environment{
        SCANNER_HOME = tool 'sonarScanner'
    }
    stages{
        stage('clean workspace') {
            steps {
                cleanWs()
            }
        }
        stage('Checkout git') {
             steps {
	            git branch: 'main', url: 'https://github.com/Ashfaque-9x/registration-app.git'
                }
            }
        stage ('Code Compile') {
	        steps {
		        sh 'mvn clean compile' 
	           }
            }
        stage('SonarQube Analysis') {
            steps{
                withSonarQubeEnv('sonarserver') {
                    sh '''${SCANNER_HOME}/bin/sonar-scanner -Dsonar.projectKey=ditiss-project \
                     -Dsonar.projectName=ditiss-project \
                     -Dsonar.exclusions=*/.java \
                     -Dsonar.login=squ_9e178c92713126b84ef17890c01b8c08ff5dadd8 '''
            }    }
        }
        
        stage("Docker Build & Push"){
             steps{
                 script{
                    withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker'){   
                        sh "docker buildx build -t devopsprojecttss ."
                        sh "docker image tag devopsprojecttss ditisssjsv/devopsprojecttss:latest "
                        sh "docker push ditisssjsv/devopsprojecttss:latest "
                     }
                }
            }
         }
         stage("TRIVY"){
             steps{
                 sh "trivy image ditisssjsv/devopsprojecttss:latest > trivyimage.txt" 
                }
            }
        stage('Deploy to k8s') {
             steps {
                script{
                     kubernetesDeploy configs: 'regapp-deploy.yml', kubeconfigId: 'kuber'
   	                }
                }
        }               
    }
}
