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
        stage("code analysis"){
           steps{
                withSonarQubeEnv('sonarqube'){
                    sh 'mvn clean verify sonar:sonar \
                    -Dsonar.projectKey=sonar-project-key \
                    -Dsonar.projectName='sonar-project' \
                    -Dsonar.host.url=http://desktop-rngufau:9000 \
                    -Dsonar.token=sqp_8a67a799818f907570147733fc2611898d82992e'
                }
            }
        }
    }     
 
}