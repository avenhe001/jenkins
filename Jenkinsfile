pipeline {
  agent any

  stages {
    stage('Validate') {
      steps {
        sh "aws cloudformation validate-template --template-body file://VPC/vpc-all-with-no-configuration-parameters.json --region 'ap-southeast-1'"
      }
    }
    
    stage('Submit Stack') {
      steps {
        sh "aws cloudformation create-stack --stack-name vpctestforaven --template-body file://VPC/vpc-all-with-no-configuration-parameters.json --region 'ap-southeast-1'"
      }
    }
  }
}