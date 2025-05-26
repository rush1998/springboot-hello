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
        stage("build & SonarQube analysis"){
            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'sonarqube') {
                    sh 'mvn clean package sonar:sonar'
                }
                }
            }
        }
    }
}
