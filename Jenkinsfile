pipeline {

    agent any
    
    parameters{
        booleanParam(defaultValue: false, description: '', name: 'sonar')
        booleanParam(defaultValue: false, description: '', name: 'deploy')
    }    
    stages {
        
        stage('build') {
            tools {
                jdk 'jdk8'
                maven 'Maven'
            }
            when {
                // Only say hello if a "greeting" is requested
                expression { params.sonar == true }
            }
            steps {   
                powershell label: '', script: 'mvn clean package'               
                withSonarQubeEnv(credentialsId: 'VMsonar') {
                            sh 'mvn sonar:sonar'
                }
            }
                
         }
        
        stage('build and deploy') {
            tools {
                jdk 'jdk8'
                maven 'Maven'
            }
            when {
                expression { params.deploy == true }
            }
            steps {
                powershell label: '', script: 'mvn clean package'
                deploy adapters: [tomcat7(credentialsId: 'tomcat-latest', path: '', url: 'http://localhost:8081/')], contextPath: 'htrip-pipeline', war: '**/*.war'
            }
        }
        
        /*stage('analysis') {
            steps {
            withSonarQubeEnv('sonar') {
                            sh 'mvn sonar:sonar'
                        }
            }
        }*/
        
        stage('archive') {
            steps {
                archive 'target/*.war'
                //echo "archived"
            }
        }
        
    }
    
}
