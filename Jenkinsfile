pipeline {
    agent any

    stages {
        stage('Checkout from git') {
            steps {
                git branch: 'prod',
                    url: 'git@github.com:Technicalkonica/enahanced-petclinc-springboot.git',
                    credentialsId: 'github-ssh'
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
