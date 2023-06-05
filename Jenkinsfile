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
    }
}