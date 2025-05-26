pipeline{
    agent any

    tools{
        maven 'maven'
    }
    stages{
        stage("Build"){
            steps{
                sh "mvn clean install"
            }
        }
        stage("SonarQube analysis"){
            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'sonarqube') {
                    sh 'mvn clean package sonar:sonar'
                }
                }
            }
        }
        stage("Quality gate"){
            steps{
                timeout(time: 2, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}
