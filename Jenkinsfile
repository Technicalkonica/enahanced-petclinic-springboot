pipeline {
    agent any
    stages {
        stage('Checkout from git') {
            steps {
                git branch:'prod',  url:'https://github.com/bkrrajmali/enahanced-petclinc-springboot.git'           
                // }
        }
        stage('Test') {
            steps {
                echo 'test'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploy'
            }
        }
    }
}
}
