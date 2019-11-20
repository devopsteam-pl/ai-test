pipeline {
    agent { label "golang" }
    options { skipDefaultCheckout() }
    stages {
        stage('CleanWorkspace') {
            steps {
                deleteDir()
            }
        }
        stage('Build') {
             steps {
                sh 'docker build .'
            }
        }
        stage('Test') {
             steps {
                sh 'echo 456'
            }
        }
    }
}
