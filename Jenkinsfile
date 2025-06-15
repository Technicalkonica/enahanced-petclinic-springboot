pipeline {
    agent any
    tools {
        maven 'maven'
    }

    stages {
        stage('Checkout from git') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Technicalkonica/enahanced-petclinic-springboot.git',
                    credentialsId: 'github-token'  // Make sure this matches the ID you set
            }
        }

        stage('Maven Compile') {
            steps {
                echo 'This is Maven Compile Stage'
                sh "mvn compile"
            }
        }

        stage('Deploy1') {
            steps {
                echo 'Deploying...'
            }
        }
    }
}
