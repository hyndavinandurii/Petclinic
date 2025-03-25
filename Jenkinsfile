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
            }
        }

        stage("Test Cases") {
            steps {
                sh "mvn test"
            }
        }

        stage("Sonarqube Analysis") {
            steps {
                sh '''$SCANNER_HOME/bin/sonar-scanner -Dsonar.url=http://34.228.19.42:9000/ -Dsonar.token=squ_d3e13953881a4d09e5cf4ad5325b85fd921a6278 -Dsonar.projectName=petclinic -Dsonar.java.binaries=. -Dsonar.projectKey=petclinic'''
            }
        }

        stage("Build") {
            steps {
                sh "mvn clean install"
            }
        }

        stage("Docker Build & Push") {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'd61dfd3a-c382-40d4-a515-83d230b5c77b', toolName: 'docker') {
                        sh "docker build -t image1 ."
                        sh "docker tag image1 venkatahyndavi/pet-clinic123:latest"
                        sh "docker push venkatahyndavi/pet-clinic123:latest"
                    }
                }
            }
        }

        stage("Deploy To Tomcat") {
            steps {
                sh "cp /var/lib/jenkins/workspace/CI-CD/target/petclinic.war /opt/apache-tomcat-9.0.65/webapps/"
            }
        }
    }
}
