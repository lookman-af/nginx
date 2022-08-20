pipeline {
    agent any
    environment {
        PROJECT_ID = 'lif-stg'
        //CLUSTER_NAME = '<<Your GKE Cluster Name>>'
        //LOCATION = '<<Your GKE Cluster Location>>'
        CREDENTIALS_ID = 'aws'
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
                    //myapp = docker.build("asia-southeast2-docker.pkg.dev/lif-stg/testing/busybox:${env.BUILD_ID}")
                     //app = docker.build("858240535111.dkr.ecr.ap-southeast-1.amazonaws.com/testing_lookman/buluxa:${env.BUILD_ID}")
                     app = docker.build("underwater")

                }
            }
        }
        stage("Push image") {
            steps {
                script {
                    docker.withRegistry('https://858240535111.dkr.ecr.ap-southeast-1.amazonaws.com/testing_lookman', 'ecr:CREDENTIALS_ID') {
                    app.push("${env.BUILD_NUMBER}")
                    app.push("latest")
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
