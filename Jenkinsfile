pipeline {
    agent { label 'slave' }
    stages {
        stage('checkout') {
            steps {
                sh 'rm -rf  hello-world-war'
                sh 'git clone https://github.com/Soumya12346/hello-world-war/'
            }
        }
        stage('build') {
            steps {
                dir(Hello-world-war)
                {
                    sh 'docker build -t image-name:1.0 .'
                }
            }
        }
        stage('deploy'){
            steps{
                sh 'docker rm -f image-name'
                sh 'docker -d -p 8080:8080 --name image-name image-name:1.0'
                
                
               sh 'ssh root@172.31.46.201'
               sh 'scp /home/slave/workspace/Samplepipeline/target/hello-world-war-1.0.0.war root@172.31.46.201:/opt/apache-tomcat-8.5.98/webapps/'
            }
        }    
    }
}
