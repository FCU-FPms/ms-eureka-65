pipeline {
    agent any
    tools { 
        maven 'Maven 3.6.3' 
        jdk 'jdk8' 
    }
    stages {
        stage ('Initialize') {
            steps {
                sh 'echo "PATH = ${PATH}"'
                sh 'echo "M2_HOME = ${M2_HOME}"'
            }
        }
        stage('Build') {
            steps {
                sh "mvn -B -DskipTests=true clean package"
            }
        }
        stage('build image') {
            steps {
                sh 'docker build --no-cache -t="franky-ms-eureka" .'
            }
        }
        stage('remove old container if exist') {
            steps {
                sh 'docker rm -f franky-ms-eureka | true'
            }
        }
        stage('use image run container') {
            steps {
                sh 'docker run --name franky-ms-eureka -d --memory 2048MB -p 50608:8888 franky-ms-eureka'
            }
        }
    }
    post { 
        always { 
            cleanWs()
        }
    }
}
