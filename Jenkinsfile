@Library("Shared") _
pipeline {
    agent { label 'vinod' }

    environment {
        PROJECT_NAME   = 'notes-app'
        IMAGE_TAG      = 'latest'
        DOCKERHUB_USER = 'durgesh040'
    }

    stages {

        stage("Clone Code") {
            steps {
                script {
                    git_clone("https://github.com/LondheShubham153/django-notes-app.git", "main")
                }
            }
        }

        stage("Build Image") {
            steps {
                script {
                    docker_build(env.PROJECT_NAME, env.IMAGE_TAG, env.DOCKERHUB_USER)
                }
            }
        }

        stage("Push Image to DockerHub") {
            steps {
                script {
                    docker_push(env.PROJECT_NAME, env.IMAGE_TAG, env.DOCKERHUB_USER)
                }
            }
        }

        stage("Test") {
            steps {
                echo "✅ Running Tests... (Placeholder)"
                // Add `pytest` or test commands if needed
            }
        }

        stage("Deploy with Docker Compose") {
            steps {
                echo "🚀 Deploying with Docker Compose..."
                sh "docker compose up -d"
            }
        }
    }

    post {
        always {
            echo "🧹 Pipeline completed. Cleaning up unused Docker resources (optional)."
            // sh "docker system prune -f" // Uncomment if you want automatic cleanup
        }
        failure {
            echo "❌ Build failed!"
        }
    }
}
