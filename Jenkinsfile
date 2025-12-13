pipeline {
    agent any

    environment {
        NEXUS_URL = "http://nexus:8081"
        NEXUS_REPO = "maven-releases"
        JAR_NAME = "demo-1.0.0.jar"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/abdallahnammoura/final-k8s-project.git'
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
                sh """
                curl -u admin:admin123 \
                --upload-file app/target/${JAR_NAME} \
                ${NEXUS_URL}/repository/${NEXUS_REPO}/${JAR_NAME}
                """
            }
        }
    }
}

