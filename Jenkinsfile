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
        stage('Security Scan with Trivy') {
            steps {
             sh 'trivy fs --format table --output trivy-report.txt --severity HIGH,CRITICAL .'
            }
        }
         stage('Sonar Analysis') {
            environment {
                 SCANNER_HOME = tool 'Sonar-scanner'
            }
            steps {
                withSonarQubeEnv('sonarserver')
                sh '''
                $SCANNER_HOME/bin/sonar-scanner \
                -Dsonar.organization=technicalkonica \
                -Dsonar.projectName=Springbootpet \
                -Dsonar.projectKEY=technicalkonica_springbootpet \
                -Dsonar.java.binaries=. \
                -Dsonar.exclusions=**/trivy-report.txt
                '''
            }
        }
}
