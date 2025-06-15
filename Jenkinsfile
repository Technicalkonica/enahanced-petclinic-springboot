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

        stage('Maven Compile') {
            steps {
                echo 'This is maven compile stage'
                sh"mvn compile"
            }
        }
        stage('Maven Test') {
            steps {
                echo 'This is maven test stage'
                sh"mvn test"
            }
       
        }
    }
}
