pipeline {
    agent any 
    
    tools {
        jdk 'jdk17'
        maven 'maven3'
    }
    
    environment{
        SCANNER_HOME= tool 'sonar-scanner'
    }
    
    stages {
        stage("Git Checkout") {
            steps {
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/hyndavinandurii/Petclinic.git'
            }
        }

        stage("Compile") {
            steps {
                sh "mvn clean compile"
                sh '''mvn sonar:sonar -Dsonar.url=http://34.228.19.42:9000/ -Dsonar.token=squ_d3e13953881a4d09e5cf4ad5325b85fd921a6278 -Dsonar.projectName=petclinic -Dsonar.java.binaries=. -Dsonar.projectKey=petclinic'''
            }
        }
