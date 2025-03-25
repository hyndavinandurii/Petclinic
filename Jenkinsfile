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
                    -Dsonar.host.url=http://34.228.19.42:9000 \
                    -Dsonar.login=squ_005280464873a00bc8a89461e35d520a1bf9ca4e\
                    -Dsonar.projectName=petclinic \
                    -Dsonar.java.binaries=. \
                    -Dsonar.projectKey=petclinic'''
    }
}

    }
}
