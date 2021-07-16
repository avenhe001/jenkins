pipeline {
  agent any 

  stages {
    stage('Switch Role') {
      steps {
        TEMP_ROLE = aws sts assume-role --role-arn arn:aws:iam::327173749814:role/cloudformation --role-session-name test
	export TEMP_ROLE
	echo $TEMP_ROLE
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