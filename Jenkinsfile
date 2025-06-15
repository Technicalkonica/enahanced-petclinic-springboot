pipeline {
    agent any

    tools {
        maven 'maven'  // Make sure this Maven tool name is configured in Jenkins
    }

    stages {
        stage('Checkout from git') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Technicalkonica/enahanced-petclinic-springboot.git',
                    credentialsId: 'github-token'
            }
        }

        stage('Maven Compile') {
            steps {
                echo 'This is Maven Compile Stage'
                sh 'mvn compile'
            }
        }

        stage('Maven Test') {
            steps {
                echo 'This is Maven Test Stage'
                sh 'mvn test'
            }
        }

        stage('File Scanning By Trivy') {
            steps {
                echo 'Trivy Scanning'
                sh 'trivy fs --format table --output trivy-report.txt --severity HIGH,CRITICAL .'
            }
        }
    }
}
