pipeline {
  agent any 

  stages {
    stage('Switch Role') {
      steps {
        sh 'TEMP_ROLE=$(aws sts assume-role --role-arn arn:aws:iam::674501369961:role/srohilla-cross-account-ecs-role --role-session-name build)'
	export TEMP_ROLE
	echo $TEMP_ROLE
	export AWS_ACCESS_KEY_ID=$(echo "${TEMP_ROLE}" | jq -r '.Credentials.AccessKeyId')
	export AWS_SECRET_ACCESS_KEY=$(echo "${TEMP_ROLE}" | jq -r '.Credentials.SecretAccessKey')
	export AWS_SESSION_TOKEN=$(echo "${TEMP_ROLE}" | jq -r '.Credentials.SessionToken')
	sh "aws cloudformation validate-template --template-body file://VPC/vpc-all-with-no-configuration-parameters.json --region 'ap-southeast-1'"
      }
    }
    stage('Validate') {
      steps {
        sh "aws cloudformation validate-template --template-body file://VPC/vpc-all-with-no-configuration-parameters.json --region 'ap-southeast-1'"
      }
    }
    
    stage('Submit Stack') {
      steps {
        sh 'TEMP_ROLE=$(aws sts assume-role --role-arn arn:aws:iam::327173749814:role/cloudformation --role-session-name test)'
	sh 'export TEMP_ROLE'
	sh 'echo $TEMP_ROLE'
        sh "aws cloudformation create-stack --stack-name vpctestforaven --template-body file://VPC/vpc-all-with-no-configuration-parameters.json --region 'ap-southeast-1'"
      }
    }
  }
}