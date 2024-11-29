pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'mechergui508/image_docker'
        DOCKER_CREDENTIALS = 'Docker_cr'
        SONARQUBE_URL = 'http://localhost:9000'
        SONARQUBE_TOKEN = credentials('sonarid')  
        NEXUS_URL = 'http://127.0.0.1:8081'
        NEXUS_REPO = 'nexus_project'
        NEXUS_USER = 'admin'
        NEXUS_PASSWORD = '123456'
    }

    stages {
        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t ${DOCKER_IMAGE}:${BUILD_NUMBER} .'
            }
        }
       
        stage('SonarQube Analysis') {
            steps {
                echo 'Running SonarQube analysis...'
                sh """
                mvn sonar:sonar -Dsonar.projectKey=mecherguisonar -Dsonar.host.url=${SONARQUBE_URL} -Dsonar.login=${SONARQUBE_TOKEN}
                """
            }
        }
        
        stage('Maven Build') {
            steps {
                echo 'Running Maven build...'
                sh 'mvn package'
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: DOCKER_CREDENTIALS, usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh """
                        echo "\$DOCKER_PASS" | docker login -u "\$DOCKER_USER" --password-stdin
                        docker push ${DOCKER_IMAGE}:${BUILD_NUMBER}
                    """
                }
            }
        }
         stage('PUSH TO NEXUS') {
        steps {
        script {
                    def file = '/target/ExamThourayaS2-0.0.1-SNAPSHOT.jar'
                    def groupId = 'com.example'
                    def artifactId = 'my-project'
                    def version = '1.0.0'
                    sh """curl -u $NEXUS_USER:$NEXUS_PASSWORD --upload-file $file $NEXUS_URL/repository/$NEXUS_REPO/$groupId/$artifactId/$version/$artifactId-$version.jar"""
                }
                }
        }
    }
}

