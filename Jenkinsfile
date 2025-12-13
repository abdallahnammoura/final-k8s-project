pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/abdallahnammoura/final-k8s-project.git'
            }
        }

        stage('Build') {
            steps {
                dir('app') {
                    sh './mvnw clean package -DskipTests'
                }
            }
        }

        stage('Upload to Nexus') {
            steps {
                sh '''
                curl -u admin:admin123 \
                --upload-file app/target/*.jar \
                http://nexus:8081/repository/maven-releases/app.jar
                '''
            }
        }
    }
}
