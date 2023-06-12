pipeline{
    agent any
    stages{
        stage('maven build'){
            steps {
                sh """
                ls -lart
                mvn install
                """
            }
        }
        stage('SonarQube analysis') {
            environment {
             SCANNER_HOME = tool'sonarScanner4.6'
            }
            steps {
                  withSonarQubeEnv('sonar-env') {
                    sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=sonar-sprig-key -Dsonar.projectName=sonar-sprig -Dsonar.sources=. -Dsonar.java.binaries=target/classes -Dsonar.sourceEncoding=UTF-8"
                }
            }

        }
        stage('SQuality Gate') {
            steps {
                timeout(time: 1, unit: 'MINUTES') {
                waitForQualityGate abortPipeline: true
                }
            }
        }    
    }    
}