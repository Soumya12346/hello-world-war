pipeline {
    agent { label 'slave' }
    stages {
        stage('checkout') {
            steps {
                sh 'git clone https://github.com/Soumya12346/hello-world-war/'
            }
        }
        stage('build') {
            steps {
                sh 'mvn --version'
                sh 'mvn clean install'
            }
        }
    }
}
