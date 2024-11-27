pipeline {
    agent any

    stages {
           
        stage('maven2.1') {
            steps {
                echo 'Running Maven build...'
                sh "mvn package"
            }
        }
    }
}
