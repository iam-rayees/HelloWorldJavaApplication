pipeline {
    agent none
    stages {
         stage('Maven Clean') {
            agent {
                docker {
                    image 'maven:3.8.6-openjdk-11'
                    // No need for label
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
                    // No need for label
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
                    args '-p 8000:8000' // Expose port
                    // No need for label
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


