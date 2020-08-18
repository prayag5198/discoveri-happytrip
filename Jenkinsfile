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
                    echo "Hello, bitwiseman!"
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
