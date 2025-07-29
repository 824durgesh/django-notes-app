@Library("Shared") _
pipeline {
    agent { label 'vinod' }

    stages {

        stage("Code") {
            steps {
                echo "📥 This is cloning the code"
                git url: "https://github.com/LondheShubham153/django-notes-app.git", branch: "main"
            }
        }

        stage("Build") {
            steps {
                script {
                    echo "🔨 Building Docker image..."
                    docker_build("notes-app", "latest", "trainwithshubham")
                }
            }
        }

        stage("Push to DockerHub") {
            steps {
                script {
                    echo "📤 Pushing Docker image..."
                    docker_push("notes-app", "latest", "durgesh040")
                }
            }
        }

        stage("Test") {
            steps {
                echo "🧪 This is testing the code"
                // You can run `pytest`, `docker exec`, or placeholder here
            }
        }

        stage("Deploy") {
            steps {
                echo "🚀 This is deploying the code using Docker Compose"
                sh "docker compose up -d"
            }
        }
    }

    post {
        success {
            echo "✅ Pipeline executed successfully!"
        }
        failure {
            echo "❌ Pipeline failed. Please check the logs."
        }
    }
}
