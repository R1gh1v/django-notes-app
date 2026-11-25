pipeline {
    agent { label "bond" }
    stages {
        stage("code") {
            steps {
                echo "this is cloning the code"
                checkout scm
                echo "cloning successful"
            }
        }
        stage("build") {
            steps {
                echo "this is building the code"
                sh "docker build -t notes-app:latest ."
            }
        }
        stage("push to docker hub") {
            steps {
                withCredentials([usernamePassword(credentialsId: "dockerHubCred", usernameVariable: "dockerHubUser", passwordVariable: "dockerHubPass")]) {
                    sh 'echo "$dockerHubPass" | docker login -u "$dockerHubUser" --password-stdin'
                    sh "docker image tag notes-app:latest r1gh1v/notes-app:latest"
                    sh "docker push r1gh1v/notes-app:latest"
                }
            }
        }
        stage("deploy") {
            steps {
                sh "docker compose up -d"
            }
        }
    }
}
