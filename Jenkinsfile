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

       stage('Sonarqube Analysis') {
          steps{
              sh '''$SCANNER_HOME/bin/sonar-scanner \
                    -Dsonar.host.url=http://3.87.153.191:9000/ \
                    -Dsonar.login=squ_fa1037721b358d2ec78079454d00602cc8d92ce1\
                    -Dsonar.projectName=petclinic \
                    -Dsonar.java.binaries=. \
                    -Dsonar.projectKey=petclinic'''
    }
}

    }
}
