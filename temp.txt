pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/anil21501/petclinic-3tier-devops.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean package -DskipTests'
            }
        }

        stage('Docker Build') {
            steps {
                bat 'docker build -t spring-petclinic .'
            }
        }

        stage('Docker Run') {
            steps {
                bat 'docker rm -f spring-petclinic-container || exit 0'
                bat 'docker run -d --name spring-petclinic-container -p 8080:8080 spring-petclinic'
            }
        }
    }
}