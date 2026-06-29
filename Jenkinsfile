pipeline{
  agent any
  environment {
    DOCKER_CRED = credentials('DockerHub')
  }
  stages
  {
    stage('fetch-code')
    {
      steps
      {
        git branch: 'main',url: 'https://github.com/Pratiksonkusare/jenkins_demo.git'
      }
    }
    stage('build-image')
    {
      steps
      {
        sh 'docker build -t chintan06/jenkins-app:${BUILD_NUMBER} .'
      }
    }
    stage('push-image')
    {
      steps
      {
        sh 'echo $DOCKER_CRED_PSW | docker login -u $DOCKER_CRED_USR --password-stdin'
        sh 'docker push chintan06/jenkins-app:${BUILD_NUMBER}'
      }
    }

    stage('update-minikube')
    {
      steps
      {
        sh 'kubectl set image deployment/pd1 jenkins-app=chintan06/jenkins-app:${BUILD_NUMBER}'
      }
    }
  }
}
        
