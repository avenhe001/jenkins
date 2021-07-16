pipeline {
  agent any

  stages {
    stage('Switch Role') {
      steps {
	- echo Build completed on `date`
	- TEMP_ROLE=$(aws sts assume-role --role-arn arn:aws:iam::327173749814:role/cloudformation --role-session-name test)
	- export TEMP_ROLE"
	- export AWS_ACCESS_KEY_ID=$(echo "${TEMP_ROLE}" | jq -r '.Credentials.AccessKeyId')
	- echo $AWS_ACCESS_KEY_ID
      }
    }
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