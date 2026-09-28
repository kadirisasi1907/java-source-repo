pipeline {
    agent any

    tools {
        maven 'Maven'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    credentialsId: 'github-credentials',
                    url: 'https://github.com/kadirisasi1907/java-source-repo.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn -version'
                bat 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }

        stage('Push Build to Repo 2') {
            steps {
                bat '''
                    git clone https://github.com/kadirisasi1907/java-build-repo.git destination-repo
                    copy target\\my-java-project-1.0-SNAPSHOT.jar destination-repo\\
                    cd destination-repo
                    git config user.name "sasivardhan"
                    git config user.email "kadirisasi923@gmail.com"
                    git add .
                    git commit -m "Add Jenkins build artifact"
                    git push origin main
                '''
            }
        }
    }
}