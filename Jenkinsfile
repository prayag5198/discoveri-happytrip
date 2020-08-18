pipeline {

    agent any
    
    options([[$class: 'JiraProjectProperty'], parameters([booleanParam(defaultValue: false, name: 'sonar'), booleanParam(defaultValue: false, name: 'deploy')]), pipelineTriggers([pollSCM('* * * * *')])])
    
    stages {
        
        stage('build') {
            tools {
                jdk 'jdk8'
                maven 'Maven'
            }
            steps {
                powershell label: '', script: 'mvn clean package'
                sh label: '', script: '''if test ${params.sonar} -eq 1 
                                            then
                                                mvn sonar:sonar
                                            fi'''
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
