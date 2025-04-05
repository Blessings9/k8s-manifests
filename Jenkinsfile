pipeline{
    agent{
        any
    }
    environment{
        APP_NAME = "album-api"
    }

    stages{
        stage("Cleanup Workspace"){
            steps{
                cleanWs()
            }
        }

        stage("Checkout from SCM"){
            steps{
                git branch: 'main', url: 'https://github.com/Blessings9/k8s-manifests.git'
            }
        }

        stage("Update the Deployment Tags"){
            steps{
                sh """
                    cat deployment.yml
                    sed -i 's/${APP_NAME}.*/${APP_NAME}:${IMAGE_TAG}/g' deployment.yml
                    cat deployment.yml
                """
            }
        }

        stage("Push the changed deployment file to Git"){
            sh """
                git config --global user.name "Blessings9"
                git config --global user.email "bmwafulirwa@gmail.com"
                git add deployment.yml
            """
            
            sh "git push https://github.com/Blessings9/k8s-manifests main"
            
        }
    }

}