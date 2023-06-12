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
                withSonarQubeEnv(credentialsId:'sat-sonar-id',installationName:'sonarqube') {
                    sh '''${SCANNER_HOME}/bin/sonar-Scanner -x\
                    -Dsonar.projectKey=projectKey \
                    -Dsonar.projectName=sonar-projectName \
                    -Dsonar.sources=. \
                    -Dsonar.java.binaries=target/classes/ \
                    -Dsonar.exclusions=./test/java/****/*.java \
                    -Dsonar.java.libraries=/var/lib/jenkins/.m2/**/*.jar \
                    // -Dsonar.projectVersion=${BUILD_NUMBER}-${GIT_COMMIT_SHORT}
                    '''
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