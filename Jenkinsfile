pipeline {
    agent any

    tools {
        nodejs 'node18'
    }

    environment {
        AWS_REGION = 'ap-south-1'
        AWS_ACCOUNT_ID = '547268988661'

        BACKEND_REPO = 'tomato-backend'
        FRONTEND_REPO = 'tomato-frontend'
        ADMIN_REPO = 'tomato-admin'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                url: 'https://github.com/akashak0717/DevOps-Project-04.git'
            }
        }

        stage('SonarQube Scan') {
            steps {
                script {
                    def scannerHome = tool 'sonar-scanner'

                    withSonarQubeEnv('SonarQube') {
                        sh """
                        ${scannerHome}/bin/sonar-scanner \
                        -Dsonar.projectKey=tomato-app \
                        -Dsonar.projectName=tomato-app \
                        -Dsonar.sources=. \
                        -Dsonar.sourceEncoding=UTF-8
                        """
                    }
                }
            }
        }

        stage('Trivy File Scan') {
            steps {
                sh 'trivy fs .'
            }
        }

        stage('Build Backend Image') {
            steps {
                sh 'docker build -t tomato-backend:latest ./backend'
            }
        }

        stage('Build Frontend Image') {
            steps {
                sh 'docker build -t tomato-frontend:latest ./frontend'
            }
        }

        stage('Build Admin Image') {
            steps {
                sh 'docker build -t tomato-admin:latest ./admin'
            }
        }

        stage('Trivy Image Scan') {
            steps {
                sh '''
                trivy image tomato-backend:latest
                trivy image tomato-frontend:latest
                trivy image tomato-admin:latest
                '''
            }
        }

        stage('Login To ECR') {
            steps {
                sh '''
                aws ecr get-login-password --region ap-south-1 | \
                docker login --username AWS --password-stdin \
                547268988661.dkr.ecr.ap-south-1.amazonaws.com
                '''
            }
        }

        stage('Tag Images') {
            steps {
                sh '''
                docker tag tomato-backend:latest \
                547268988661.dkr.ecr.ap-south-1.amazonaws.com/tomato-backend:latest

                docker tag tomato-frontend:latest \
                547268988661.dkr.ecr.ap-south-1.amazonaws.com/tomato-frontend:latest

                docker tag tomato-admin:latest \
                547268988661.dkr.ecr.ap-south-1.amazonaws.com/tomato-admin:latest
                '''
            }
        }

        stage('Push Images To ECR') {
            steps {
                sh '''
                docker push 547268988661.dkr.ecr.ap-south-1.amazonaws.com/tomato-backend:latest

                docker push 547268988661.dkr.ecr.ap-south-1.amazonaws.com/tomato-frontend:latest

                docker push 547268988661.dkr.ecr.ap-south-1.amazonaws.com/tomato-admin:latest
                '''
            }
        }

        stage('Update Kubeconfig') {
            steps {
                sh '''
                aws eks update-kubeconfig \
                --region ap-south-1 \
                --name tomato-eks
                '''
            }
        }

        stage('Deploy To EKS') {
            steps {
                sh '''
                kubectl rollout restart deployment/backend-deployment
                kubectl rollout restart deployment/frontend-deployment
                kubectl rollout restart deployment/admin-deployment
                '''
            }
        }

        stage('Verify Deployment') {
            steps {
                sh '''
                kubectl get pods
                kubectl get svc
                '''
            }
        }
    }

    post {
        success {
            echo 'Tomato Application Successfully Deployed To EKS'
        }

        failure {
            echo 'Pipeline Failed'
        }

        always {
            cleanWs()
        }
    }
}