pipeline {
    agent any
    stages {
        stage("checkout"){
            steps{
                script{
                     git url: "https://github.com/dinesh-adlus/main-repo.git"
                }
            }
        }
       stage("Generating OIDC token and saving it to a file") {
            steps {
                script {
                        sh (script: 'gcloud auth print-identity-token main-service-account@splendid-sonar-427819-i0.iam.gserviceaccount.com  --audiences="//iam.googleapis.com/projects/92076150966/locations/global/workloadIdentityPools/jenkins-pool/subject/SUBJECT_ATTRIBUTE_VALUE"  > C:/Users/dini/Downloads',returnStdout: true)
                }                                                                                                                                                                                                                                                                                                                                                                                            
            }
        }
        stage ("getting the WIF config file into a variable")
        {
            steps {
                     withCredentials([file(credentialsId: 'wif-config-file', variable: 'WIF')]) 
                        {
                         sh '''
                            gcloud auth login --brief --cred-file=$WIF --quiet
        					 ls
        					 gsutil cp app.yaml ./dist/design1
        					 gsutil cp package.json ./dist/design1
                            '''

                        }
                }
        }
    }    
}
