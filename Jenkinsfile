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
                sh 'mvn --version'
                sh 'mvn clean install'
            }
        }
        stage('deploy'){
            steps{
                sh 'ssh root@172.31.47.22'
                sh 'scp /home/slave1/workspace/Samplepipeline/target/hello-world-war-1.0.0.war  root@172.31.47.22:/opt/apache-tomcat-8.5.98/webapps'
            }
        }    
    }
}
