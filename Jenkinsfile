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
             SCANNER_HOME = tool 'sonar-scaner'
            }
            steps {
                withSonarQubeEnv(credentialsId: 'sat-sonar-id', installationName: 'sonarqube') {
                    sh '''$SCANNER_HOME/bin/sonar-scaner \
                    -Dsonar.projectKey=projectKey \
                    -Dsonar.projectName=sonar-projectName \
                    -Dsonar.sources=src/ \
                    -Dsonar.java.binaries=target/classes/ \
                    -Dsonar.exclusions=src/test/java/****/*.java \
                    -Dsonar.java.libraries=/var/lib/jenkins/.m2/**/*.jar \
                    -Dsonar.projectVersion=${BUILD_NUMBER}-${GIT_COMMIT_SHORT}'''
                }
            }

        }
    }    
 
}