def gv

pipeline {
    agent any
    parameters {

    choice(name:'VERSION' , choices: ['1','2','3'])
    booleanParam(name : "execute" , defaultValue: true )
    }
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
            when {
                expression {
                        params.execute
                }
            }
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
                     echo "deploying"
                     echo "deploying version ${params.VERSION}"
                    //gv.deployApp()
                }
            }
        }
    }
}