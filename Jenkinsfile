pipeline {
    agent { label "openshift-common" }
    options { skipDefaultCheckout() }
    stages {
        stage('CleanWorkspace') {
            steps {
                deleteDir()
            }
        }
        stage('Build') {
            steps {
              script {
                  openshift.withCluster() {
                        openshift.withProject('cicd') { 
                            openshift.withCredentials('cicd-my-prilvileged-token-id') {
                                //openshift.verbose(true)   
                                echo "${openshift.raw( "version" ).out}"
                                echo "In project: ${openshift.project()}"
                                //echo "${openshift.raw("whoami")}"
                                def dc = openshift.selector('dc', "gitea")
                                dc.rollout().latest()    
                                dc.rollout().status()
                            }
                        }
                  }
              }
            }
        }
        
    }
}

