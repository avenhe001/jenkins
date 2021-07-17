pipeline {
  agent any 

  stages {
    stage('Switch Role') {
      steps {
        withAWS(roleAccount:'327173749814', role:'cloudformation') {
		sh "aws cloudformation validate-template --template-body file://VPC/vpc-all-with-no-configuration-parameters.json --region 'ap-southeast-1'"	
	}
      }
    }
    
    stage('Submit Stack') {
      steps {
        withAWS(roleAccount:'327173749814', role:'cloudformation') {
		if(sh(script: """ aws cloudformation describe-stacks --stack-name vpctestforaven1 --region 'ap-southeast-1' --query 'failures[0].reason' --output text""",returnStdout: true).trim()){
		  echo 'aaa'
		}
		else{
		  echo 'bbb'
		}			
	}
      }
    }
  }
}
