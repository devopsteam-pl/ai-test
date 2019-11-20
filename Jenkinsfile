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
                 openshift.withCluster() {
                    sh "git clone http://gitea.192.168.42.104.nip.io/krdian/test-repo.git ."
                    //sh " make clean generate build"
                }
            }
        }
    }
}
