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
            //when {
                // Only say hello if a "greeting" is requested
             //   expression { params.sonar == true }
            //}
            steps {   
                    //powershell label: '', script: 'mvn clean package'
                script {
                    if (params.sonar == true) {
                        powershell label: '', script: 'mvn clean package'
                        //echo 'I only execute on the master branch'
                    }
                }
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
