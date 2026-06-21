pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                url: 'https://github.com/akashak0717/DevOps-Project-04.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Build Stage'
            }
        }

    }
}