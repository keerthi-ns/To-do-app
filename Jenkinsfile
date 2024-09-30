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
                   withDockerRegistry(credentialsId: '9ea0c4b0-721f-4219-be62-48a976dbeec0') {
                    sh "docker build -t  todoapp:latest -f backened/Dockerfile . "
                    sh "docker tag todoapp:latest keerthins123/todoapp:latest "
                 }
               }
            }
        }

        stage('Docker Push') {
            steps {
               script{
                   withDockerRegistry(credentialsId: '9ea0c4b0-721f-4219-be62-48a976dbeec0') {
                    sh "docker push  keerthins123/todoapp:latest "
                 }
               }
            }
        }
		stage('Deploy to Docker') {
            steps {
               script{
                   withDockerRegistry(credentialsId: '9ea0c4b0-721f-4219-be62-48a976dbeec0') {
                    sh "docker run -d --name to-do-app -p 4000:4000 keerthins123/todoapp:latest "
                 }
               }
            }
        }

    }
}
