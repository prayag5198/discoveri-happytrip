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
                //powershell label: '', script: 'mvn clean package'
                script{
                if (${params.sonar} == 1) {
                    mvn clean install
                    mvn sonar:sonar
                }
                }
               // if test ${params.sonar} -eq 1 
                //                    then
                 //                               deploy contextPath: 'htrip-pipeline', war: '**/*.wa'
                  //                          fi'''
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
