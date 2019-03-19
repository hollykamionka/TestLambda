pipeline {
  stages {
    stage ('zip') {
      steps() {
        sh 'zip mylambda.zip mylambda.py'
      }
    }
    stage ('deliver') {
      steps() {
        sh 'aws s3 cp target/mylambda.zip s3://sme-artifact-bucket/mylambda.zip --region us-west-2'
      }
    }  
    stage ('deploy') {
      steps() {
        sh '''aws cloudformation create-stack --stack-name mylambdatest1 --template-body file://mylambda.template --capabilities CAPABILITY_IAM --region us-west-2
          aws cloudformation wait stack-create-complete --stack-name mylambdatest1 --region us-west-2
          aws cloudformation describe-stack-events --stack-name mylambdatest1 --region us-west-2'''
      }
    }    
  }
}
            