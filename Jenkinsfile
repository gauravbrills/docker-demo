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
        failure {
            mail to: grawat@sapient.com, subject: 'The Pipeline build failed :('
        }
    }
 }
  
