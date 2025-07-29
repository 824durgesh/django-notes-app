pipeline {
    agent { label 'vinod' }
    
    stages {
        
        stage("Code") {
            steps {
                echo "This is cloning the code"
                git url: "https://github.com/LondheShubham153/django-notes-app.git", branch: "main"
            }
        }
        stage("Build") {
            steps {
                script {
                    docker_build("notes-app","latest","trainwithshubham")
                }
            }
        }
        stage("Push to DockerHub") {
            steps {
                script {
                    docker_push("notes-app","latest","durgesh040")
                }
            }
        }
        stage("Test") {
            steps {
                echo "This is testing the code"
            }
        }
        stage("Deploy") {
            steps {
                echo "This is deploying the code"
                sh "docker compose up -d"
            }
        }
    }
}
