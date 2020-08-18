pipeline {

    agent any
    
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
        
        stage('archive') {
            steps {
                archive 'target/*.war'
                //echo "archived"
            }
        }
        
    }
    
}
