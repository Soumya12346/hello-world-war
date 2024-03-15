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
            }
        }    
    }
}
