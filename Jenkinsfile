pipeline {
    agent any

    stages {
        stage('Checkout from git') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Technicalkonica/enahanced-petclinic-springboot.git',
                    credentialsId: 'github-token'  // Make sure this matches the ID you set
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying...'
            }
        }
    }
}
