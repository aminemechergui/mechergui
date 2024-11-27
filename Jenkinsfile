pipeline {
    agent any

    stages {
        stage('checkout GIT') {
            steps {
                echo 'Pulling code from Git ...'
                git branch: 'master', 
                url: 'https://github.com/aminemechergui/mechergui.git'
            }
        }
        
        stage('maven') {
            steps {
                echo 'Running Maven build...'
                sh "mvn package"
            }
        }
    }
}
