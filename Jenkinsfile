 pipeline {
        agent any

        tools{
                maven "Maven"
        }

        stages {
          stage("build & SonarQube analysis") {
            agent any
            steps {
              withSonarQubeEnv('sonarqube') {
                sh 'mvn clean package sonar:sonar'
              }
            }
          }
          stage("Quality Gate") {
            steps {
              timeout(time: 1, unit: 'HOURS') {
                waitForQualityGate abortPipeline: true
              }
            }
          }
         
         stage("Maven Packaging"){
          steps{
           sh 'mvn package'
          }
         }
         
         stage("Build Image") {
          steps{
           sh 'docker build -t java-maven-app:1.0 .'
          }
         }
         
         stage("Logging Into ECR"){
         steps{
           sh 'aws ecr get-login-password --region ap-northeast-1 | docker login --username AWS --password-stdin 266454083192.dkr.ecr.ap-northeast-1.amazonaws.com'
         } 
         }
         
         stage("Pushing Image To ECR"){
          steps{
           sh 'docker tag java-maven-app:1.0 266454083192.dkr.ecr.ap-northeast-1.amazonaws.com/maven-app:1.0'
           sh 'docker push 266454083192.dkr.ecr.ap-northeast-1.amazonaws.com/maven-app:1.0'
          }
         }
         
         stage("Logging Out ECR"){
          steps{
           sh 'docker logout'
          }
         }
         
        }
 }
