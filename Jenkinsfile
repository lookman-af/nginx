pipeline {
    agent any
    environment {
        PROJECT_ID = 'indigo-tracker-356505'
        //CLUSTER_NAME = '<<Your GKE Cluster Name>>'
        //LOCATION = '<<Your GKE Cluster Location>>'
        CREDENTIALS_ID = 'gcr-registry'
    }
    stages {
        stage("Checkout code") {
            steps {
                checkout scm
            }
        }
        stage("Build image") {
            steps {
                script {
                    myapp = docker.build("asia.gcr.io/indigo-tracker-356505/busybox:${env.BUILD_ID}")
                }
            }
        }
        stage("Push image") {
            steps {
                script {
                    docker.withRegistry('https://asia.gcr.io', 'gcr-registry') {
                            myapp.push("latest")
                            myapp.push("${env.BUILD_ID}")
                    }
                }
            }
        }        
      //  stage('Deploy to GKE') {
       //     steps{
        //        sh "sed -i 's/hello:latest/hello:${env.BUILD_ID}/g' deployment.yaml"
       //         step([$class: 'KubernetesEngineBuilder', projectId: env.PROJECT_ID, clusterName: env.CLUSTER_NAME, location: env.LOCATION, manifestPattern: 'deployment.yaml', credentialsId: env.CREDENTIALS_ID, verifyDeployments: true])
         //   }
        //}
    }    
}
