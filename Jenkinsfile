pipeline {
    agent none
    stages {
        stage('Checkout') {
            agent {
                docker {
                    image 'alpine/git'
                    label 'docker-agent'
                }
            }
            steps {
                checkout scm
            }
        }

        stage('Maven Clean') {
            agent {
                docker {
                    image 'maven:3.8.6-openjdk-11'
                    label 'docker-agent'
                }
            }
            steps {
                sh 'mvn clean'
            }
        }

        stage('Build with Maven') {
            agent {
                docker {
                    image 'maven:3.8.6-openjdk-11'
                    label 'docker-agent'
                }
            }
            steps {
                sh 'mvn package'
            }
        }

        stage('Run Spring Boot Application') {
            agent {
                docker {
                    image 'maven:3.8.6-openjdk-11'
                    label 'docker-agent'
                    args '-p 8080:8080'
                }
            }
            steps {
                sh 'mvn spring-boot:run'
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}

