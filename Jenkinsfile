pipeline {
    agent any
    stages {
        stage('Build Backend') {
            steps {
                bat 'mvn package DskipTests=true'
            }
        }
        stage('Unit Tests') {
            steps {
                bat 'mvn test'
            }
        }

        stage('Sonar Analysis') {
            environment {
                scannerHome = tool 'SONAR_SCANNER'
            }
            steps {
                withSonarQubeEnv('SONAR_LOCAL') {
                    bat "${scannerHome}/bin/sonar-scanner -e -Dsonar.projectKey=DeployBackend -Dsonar.host.url=http://localhost:9000 -Dsonar.login=22774aa3cbe86b70ee9040113231d5120bf5765c -Dsonar.java.binaries=target"
                }
            }
        }
}}
