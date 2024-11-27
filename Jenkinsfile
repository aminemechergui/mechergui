pipeline {
    agent any

    stages {
           
        stage('maven2') {
            steps {
                echo 'Running Maven build...'
                sh "mvn package"
            }
        }
    }
}
