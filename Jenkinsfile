pipeline {
    agent any
    stages {
            stage('Package Application') {
                steps {
                    echo 'Packaging the app into jars with maven'
                    sh "./mvnw clean package"
                }
            }
            stage('Build App Docker Images') {
                        steps {
                            echo 'Building App Dev Images'
                            sh "docker build -t acydevops/todoserver ."
                            sh 'docker push acydevops/todoserver'
                            sh "docker build -t acydevops/todoapp ."
                            sh 'docker push acydevops/todoapp'                
                        }
                    }

            stage('Deploy App on Kubernetes Cluster'){
            steps {
                echo 'Deploying App on Kubernetes Cluster'
                sh 'kubectl apply -f docker-compose.yml'
                
            }
    }
}
}