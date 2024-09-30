pipeline {
    agent any

    stages {
        stage('git-checkout') {
            steps {
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/keerthi-ns/To-do-app.git'
            }
        }


         stage('Docker Build') {
            steps {
               script{
                   withDockerRegistry(credentialsId: '2969c022-3f74-4d87-a3c9-02cd3a2cfef9') {
                    sh "docker build -t  todoapp:latest -f backend/Dockerfile . "
                    sh "docker tag todoapp:latest keerthins123/todoapp:latest "
                 }
               }
            }
        }

        stage('Docker Push') {
            steps {
               script{
                   withDockerRegistry(credentialsId: '2969c022-3f74-4d87-a3c9-02cd3a2cfef9') {
                    sh "docker push  keerthins123/todoapp:latest "
                 }
               }
            }
        }
		stage('Deploy to Docker') {
            steps {
               script{
                   withDockerRegistry(credentialsId: '2969c022-3f74-4d87-a3c9-02cd3a2cfef9') {
                    sh "docker run -d -p 4000:4000 --name to-do-app keerthins123/todoapp:latest"
                 }
               }
            }
        }

    }
}
