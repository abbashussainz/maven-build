def gv

pipeline {
    agent any
    stages {
        stage("init") {
            steps {
                script {
                    gv = load "script.groovy"
                }
            }
        }
        stage("build jar") {
            steps {
                script {
                    echo "building jar"
                    //gv.buildJar()
                }
            }
        }
        stage("build image") {
            steps {
                script {
                    echo "building image"
                    //gv.buildImage()
                }
            }
        }
        stage("deploy") {
            steps {
                script {
                     withCredentials([
                     usernamePassword(credentials: 'github-cred' , usernameVaraible: USER , passwordVaraible: PWD)
                     ]){
                        echo "${USER} ${PWD}"
                     }
                     echo "deploying"
                    //gv.deployApp()
                }
            }
        }
    }   
}