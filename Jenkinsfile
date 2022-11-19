 pipeline {
        agent none

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
         
         stage("maven packaging"){
          steps{
           sh 'mvn clean package'
          }
         }
        }
 }
