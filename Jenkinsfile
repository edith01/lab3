pipeline {
    agent any

    stages {
stage('Cloning Repo and generating Startup script and moving file to bucket') {
            steps {
                echo 'Cloning the Repo'
                sh 'rm -fr lab3'
                sh 'git clone https://github.com/edith01/lab3.git'
                withCredentials([file(credentialsId: 'gcloud-creds', variable: 'GCLOUD_CREDS')]) {
        
                    sh 'gsutil -m cp -r /var/lib/jenkins/workspace/lab3/* gs://test1lab/'
                }
                sh "gcloud compute ssh  imranc42@instance-1 --zone=us-central1-a --command 'sudo apt install apache2 -y'"
            }
        }
        stage('Moving to production & Deploying') {
            steps {
   
                sh "gcloud compute ssh  imranc42@instance-1 --zone=us-central1-a --command 'sudo rm -rf /var/www/html/* ;sudo mv /var/lib/jenkins/workspace/lab3/lab3/* /var/www/html/'"

                
            }
           stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
