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
            
            steps {
                powershell label: '', script: 'mvn clean package'
            }
                
         }
        
        stage('sonar') {
            tools {
                jdk 'jdk8'
                maven 'Maven'
            }
            when {
                expression { params.sonar == true }
            }
            steps {                  
                withSonarQubeEnv('sonar') {
                      powershell label: '', script: 'mvn sonar:sonar'
                }
            }
        }
        stage('deploy') {        
            when {
                expression { params.deploy == true }
            }
            steps {
                deploy adapters: [tomcat7(credentialsId: 'tomcat-latest', path: '', url: 'http://localhost:8081/')], contextPath: 'htrip-pipeline', war: '**/*.war'
            }
        }
        
        
        stage('archive') {
            steps {
                archive 'target/*.war'
                //echo "archived"
            }
        }
        
    }
    
}
