pipeline {
    agent any

    stages {
           
        stage('maven2.2') {
            steps {
                echo 'Running Maven build...'
                sh "mvn package"
            }
        }
    }
}
