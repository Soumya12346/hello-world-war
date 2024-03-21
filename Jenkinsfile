pipeline {
    agent { label 'docker' }
    environment {     
        DOCKERHUB_CREDENTIALS= credentials('dockerhubcredentials')     
    }
    stages {
        stage('Checkout') {
            steps {
                sh 'rm -rf hello-world-war'
                sh 'git clone https://github.com/Soumya12346/hello-world-war.git'
            }
        }
		
        stage('Build') {
            steps {
                sh 'echo "inside build"'
                dir("hello-world-war") {
                    sh 'echo "inside dir"'    
                    sh 'docker build -t tomcat-file:${BUILD_NUMBER} .'
                }
            }
        }
		
        stage('Login to Docker Hub') {         
            steps {                            
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'                 
                echo 'Login Completed'                
            }           
        }
        
        stage('Push Image to Docker Hub') {         
            steps {  
                sh "docker tag tomcat-file:${BUILD_NUMBER} soumya12346/myubuntu:${BUILD_NUMBER}"
                sh "docker push soumya12346/myubuntu:${BUILD_NUMBER}"                 
                echo 'Image pushing completed..'       
            }           
        }
        
        stage('Pull and Deploy') {
            parallel {
                stage('Deploy to node1') {
                    agent { label 'node1' }
                    steps {
                        sh "docker pull soumya12346/myubuntu:${BUILD_NUMBER}"
                        sh "docker run -d --name my_container_1 -p 8085:8080 soumya12346/myubuntu:${BUILD_NUMBER}"
                    }
                }
                stage('Deploy to any') {
                    agent { label 'slave2' }
                    steps {
                        sh "docker pull soumya12346/myubuntu:${BUILD_NUMBER}"
                        sh "docker run -d --name my_container_2 -p 8086:8080 soumya12346/myubuntu:${BUILD_NUMBER}"
                    }
                }
            }
        }
    }
}
