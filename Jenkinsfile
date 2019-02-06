pipeline{
 agent any
 parameters {
        string(name: 'dockerRepo', defaultValue: '550640273869.dkr.ecr.us-east-1.amazonaws.com/myapp', description: 'Docker Repository ?')
    }
 stages{
   stage('build'){
    steps{
      echo 'Starting docker build'
      sh "echo dockerRepo= ${params.dockerRepo}"
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
  
