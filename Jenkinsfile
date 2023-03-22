pipeline {
    agent any

    environment {
    DOCKER_PASSWORD = credentials('DOCKER_PASSWORD')


    }
    stages {

            stage('Build Artifact') {
                        steps {
                            echo 'Building Artifact'
                            sh 'chmod +x ./todoserver/mvnw'
                            sh 'cd todoserver && ./mvnw clean package -DskipTests'                            
                            sh "cd todoserver && cp target/todo-server-0.0.1.jar release"

                        }
                    }
            stage('Build App Docker Images') {
                        steps {
                            echo 'Building App Dev Images'
                            sh 'echo $DOCKER_PASSWORD | docker login -u acydevops --password-stdin'
                            sh "docker build -t acydevops/todoserver -f ./todoserver/Dockerfile ./todoserver"
                            sh 'docker push acydevops/todoserver'
                            sh "docker build -t acydevops/todoapp -f ./todoapp/Dockerfile ./todoapp"
                            sh 'docker push acydevops/todoapp'
                        }
                    }

      
           stage('Deploy App on Kubernetes cluster'){
                        steps {
                            echo 'Deploying App on Kubernetes'
                            ansiblePlaybook credentialsId: 'cihat', disableHostKeyChecking: true, installation: 'ansible', inventory: 'inventory.txt', playbook: 'k8sdeployplaybook.yml'
            }
        }     
        }     
            
    }