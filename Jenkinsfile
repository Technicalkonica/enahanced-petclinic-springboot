pipeline {
    agent any

    stages {
        stage('Checkout from git') {
            steps {
                git branch: 'prod', url: 'https://github.com/Technicalkonica/enahanced-petclinc-springboot.git'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
            }
        }
    }
}
