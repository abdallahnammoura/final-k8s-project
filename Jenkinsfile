pipeline {
    agent any

    environment {
        NEXUS_URL  = "http://nexus:8081"
        NEXUS_REPO = "maven-releases"
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
                    sh 'chmod +x mvnw'
                    sh './mvnw clean package -DskipTests'
                }
            }
        }

        stage('Upload to Nexus') {
            steps {
                sh '''
                JAR_FILE=$(ls app/target/*.jar | head -n 1)
                BASENAME=$(basename $JAR_FILE)

                curl -u admin:admin123 \
                  --upload-file $JAR_FILE \
                  ${NEXUS_URL}/repository/${NEXUS_REPO}/$BASENAME
                '''
            }
        }
    }
}

