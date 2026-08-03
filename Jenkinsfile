pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/anil21501/petclinic-3tier-deveops.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t spring-petclinic .'
            }
        }

        stage('Docker Run') {
            steps {
                sh 'docker rm -f spring-petclinic-container || true'
                sh 'docker run -d --name spring-petclinic-container -p 8080:8080 spring-petclinic'
            }
        }
    }
}
