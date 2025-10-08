pipeline {
    agent any

    tools {
        maven 'maven-app'
    }

    stages {
        stage('Build jar') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Build Image') {
            steps {
                script {
                    echo "Building the Docker image..."
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-cred', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                        sh 'docker build -t kavintito/demo-app:jmp-2.0 .'
                        sh "echo \$PASS | docker login -u \$USER --password-stdin"
                        sh 'docker push kavintito/demo-app:jmp-2.0'
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    echo "Deploying the application..."
                }
            }
        }
    }
}
