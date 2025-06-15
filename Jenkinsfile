pipeline {
    agent any

    tools {
        maven 'Maven'  // This assumes you have Maven installed in Jenkins tool configuration
    }

    environment {
        IMAGE_NAME = 'your-image-name'  // Define the image name
        IMAGE_TAG = 'latest'  // Define the image tag (or set it dynamically)
        TENANT_ID = "79e070eb-19f3-4ea9-840b-5be5ac643d55"  // Replace with your actual Tenant ID
        ACR_REGISTRY_NAME = "Bootcamp"  // Replace with your actual ACR registry name
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
                echo 'Running security scan with Trivy'
                sh 'trivy fs --format table --output trivy-report.txt --severity HIGH,CRITICAL .'
            }
        }

        stage('Sonar Analysis') {
            environment {
                SCANNER_HOME = tool 'Sonar-scanner'
            }
            steps {
                withSonarQubeEnv('sonarserver') {
                    sh '''
                    /var/lib/jenkins/tools/hudson.plugins.sonar.SonarRunnerInstallation/Sonar-scanner/bin/sonar-scanner \
                    -Dsonar.organization=technicalkonica \
                    -Dsonar.projectName=Springbootpet \
                    -Dsonar.projectKey=technicalkonica_springbootpet \
                    -Dsonar.java.binaries=target/classes \
                    -Dsonar.exclusions=**/trivy-report.txt
                    '''
                }
            }
        }

        stage('Maven Package') {
            steps {
                echo 'This is Maven package stage'
                sh "mvn package"  // Corrected command from 'mvn packaged' to 'mvn package'
            }
        }

        stage('Docker Build') {
            steps {
                script {
                    echo 'This is Docker Build start'
                    docker.build("$IMAGE_NAME:$IMAGE_TAG")  // Using variables for image name and tag
                }
            }
        }

        stage('Azure Login to ACR') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'azurespn', usernameVariable: 'ACR_USERNAME', passwordVariable: 'ACR_PASSWORD')]) {
                    script {
                        // Log in to Azure CLI
                        sh 'az login --service-principal -u $ACR_USERNAME -p $ACR_PASSWORD --tenant $TENANT_ID'
                        
                        // Log in to ACR (Azure Container Registry)
                        sh 'az acr login --name $ACR_REGISTRY_NAME'
                    }
                }
            }
        }
    }
}
