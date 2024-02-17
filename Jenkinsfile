pipeline {
    /* agent {
        docker {
            image 'maven:3.9.0'
            args '-v /root/.m2:/root/.m2'
        }
    } */
    agent any
    tools { 
        maven 'maven 3.3.9' 
        jdk 'jdk'
        node 'nodejs'
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm --version'
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}
