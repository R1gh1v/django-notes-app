@Library("Shared") _
pipeline {
    agent { label "bond" }
    stages {
        stage("hello") {
            steps {
                script {
                    hello()
                }
            }
        }
        stage("code") {
            steps {
                script {
                    clone("https://github.com/r1gh1v/django-notes-app.git", "main")
                }
            }
        }
        stage("build") {
            steps {
                script {
                    docker_build("notes-app", "latest", "r1gh1v")
                }
            }
        }
        stage("push to docker hub") {
            steps {
                script {
                    docker_push("notes-app", "latest", "r1gh1v")
                }
            }
        }
        stage("deploy") {
            steps {
                echo "this is deploying the code"
                sh "docker compose up -d"
            }
        }
    }
}
