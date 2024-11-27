pipeline {
    agent any

    stages {
           
        stage('maven3') {
            steps {
                echo 'Running Maven build...'
                sh "mvn package"
            }
        }
    }
}
