
@Library("Shared") _

pipeline {
    agent {label "agent-2"}

    stages {
        stage('Hello'){
            steps{
                hello()
            }
        }
        
        stage('Code') {
            steps {
                script {
                      clone('https://github.com/RajeelSiddiqui1/django-note-app.git',"main")
                }
                
            }
        }
        
        stage('Build') {
            steps {
               script{
                   docker_build("notes-app", "latest", "rajeel")
               }
            }
        }
        
        stage('Push on Docker Hub') {
            steps {
               script{
                   docker_push("notes-app","latest","rajeel")
               }
            }
        }
        
        stage('Deploy') {
            steps {
                script{
                    docker_compose()
                }
            }
        }
        
    }
    post {
        always {
            script {
                echo 'Cleaning up space in ubuntu'
                clean_docker_space()
            }
        }
    }
}
