pipeline {
    agent any

    tools {
        maven 'Maven'  // This assumes you have Maven 3.6.3 installed in Jenkins tool configuration
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
                echo 'This is Maven compile stage'
                sh "mvn compile"  // Add space between sh and the command
            }
        }

        stage('Maven Test') {
            steps {
                echo 'This is Maven test stage'
                sh "mvn test"  // Add space between sh and the command
            }
        }
    }
}
