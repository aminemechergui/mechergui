pipeline {
    agent any

    stages {
           
        stage('maven') {
            steps {
                echo 'Running Maven build...'
                sh "mvn package"
            }
        }
    }
}
