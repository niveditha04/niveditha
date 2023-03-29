pipeline {
    agent any
    tools { 
    maven 'maven3'
    stages {
        stage('source code') {
            steps {
                git credentialsId: 'git', url: 'https://github.com/niveditha04/niveditha.git'
            }
        }
        stage('compile') {
            steps {
                sh 'mvn clean compile'
            }
        }
        stage('test') {
            steps {
                sh 'mvn clean test'
            }
        }
        stage('package') {
            steps {
                withSonarEnv('sonar')
                sh 'mvn clean package sonar:sonar'
            }
        }
        stage('deploy') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://52.201.240.253:8090/')], contextPath: null, war: '"**/*.war"'
                
                
            }
        }

        
        
        
    }
}
