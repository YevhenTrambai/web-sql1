pipelne {
  agent any

  environment {
  DOCKER_CREDENTIALS_ID = 'docker-credentials-id' 
  DOCKER_IMAGE = "yevhentrambai/web-sql"
  }
stages{
stage('clone repository') {
  steps {
    git branch: 'main', url: 'https://github.com/YevhenTrambai/web-sql1.git'
}
}
stage('build docker image'){
  steps {
    script {
      docker.build(DOCKER_IMAGE)
    }
  }
}
stage('run test'){
  steps{
    script {
      sh "echo 'run some tests'"
   }
  }
} 
stage('push to docker hub'){
  when {
    expression {currentBuild.currentResult == 'SUCCESS'}
  }
  steps {
    script {
      docker.withRegistry('https://index.docker.io/v1', DOCKER_CREDENTIALS_ID) {
        docker.image(DOCKER_IMAGE).push()
      }
    }
  }
} 
post {
  failure {
    echo "Build or test failed"
    }
  } 
}
