pipeline {
    agent any
    stages {
//      stage('Checkout'){
//        steps{
//          git 'git@github.com:rakeshkorukonda2412/ultimate-list-image.git'
//        }
//      }
      stage('Build Backend Image'){
       steps{
        script{
          docker.withRegistry('https://docker.io', 'dockerhub-cred') {
            echo 'building application'
            def customImage = docker.build("docker.io/rakeshkoru91/uloe-server:${env.BUILD_ID}","--target server -f Dockerfile .")
            //customImage.push()
          }
        }
       }
      }
      stage('Anchor-CLI Backend image scan'){
        steps{
           sh "Secutiry scan of backend images"
        }
      }
      stage('Build Frontend Image'){
       steps{
        script{
          docker.withRegistry('https://docker.io', 'dockerhub-cred') {
            echo 'building application'
            def customImage = docker.build("docker.io/rakeshkoru91/uloe-frontend:${env.BUILD_ID}","--target frontend -f Dockerfile .")
            //customImage.push()
          }
        }
       }
      }
      stage('Anchor-CLI frontend image scan'){
        steps{
           sh "Secutiry scan of frontend images"
        }       
      }
      stage('Push Image'){
        steps{
         script{
           docker.withRegistry('https://docker.io', 'dockerhub-cred') {
            docker.image("docker.io/rakeshkoru91/uloe-server:${env.BUILD_ID}").push()
            docker.image("docker.io/rakeshkoru91/uloe-frontend:${env.BUILD_ID}").push()
          }
        }
      }      
  }
}
}
