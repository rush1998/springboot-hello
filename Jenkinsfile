pipeline{
    agent any

    tools{
        maven 'maven'
    }
    enviornment {
        registry = '334973675402.dkr.ecr.us-east-1.amazonaws.com/springboot'
        registryCredential = 'jenkins-ecr-login-credentials'
        dockerimage = ''
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
        stage('Building the Image') {
        steps {
            script {
            def dockerImage = docker.build("${registry}:${BUILD_NUMBER}")
        }
    }
    }
    }
}
