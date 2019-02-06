pipeline{
 agent any
 options([
    buildDiscarder(logRotator(daysToKeepStr: '4', numToKeepStr: '2')),
])
 parameters {
        string(name: 'DOCKER_REPO', defaultValue: '550640273869.dkr.ecr.us-east-1.amazonaws.com/myapp', description: 'Docker Repository ?')
        string(name: 'IMAGE_TAG', defaultValue: '2019.01.01', description: 'Docker Image Tag ?')
    }
 stages{
   stage('build'){
    steps{
      echo 'Starting docker build'
      sh "echo dockerRepo= ${params.DOCKER_REPO}"      
      sh "docker build -t 550640273869.dkr.ecr.us-east-1.amazonaws.com/myapp:${GIT_COMMIT} ."
      sh '''
          eval  "\\$(aws ecr get-login --no-include-email --region us-east-1)""
         '''
      echo "build complete , pushing image to [${params.DOCKER_REPO}]"
      sh "docker push ${params.DOCKER_REPO}:${params.IMAGE_TAG}"
     }
   }
  }
  post {
        always {
            echo 'One way or another, I have finished'
            deleteDir() /* clean up our workspace */
        }
        success {
            echo 'I succeeeded!'
        }
        unstable {
            echo 'I am unstable :/'
        }
        failure {
            echo 'I failed :('
        }
        changed {
            echo 'Things were different before...'
        }
    }
 }
  
