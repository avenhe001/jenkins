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
		string count = sh(script: """ aws cloudformation list-stacks --stack-status-filter CREATE_COMPLETE --region 'ap-southeast-1'""")
		echo count
		string status = sh(script: """ aws cloudformation describe-stacks --stack-name vpctestforaven --region 'ap-southeast-1' --query 'failures[0].reason' --output text""",returnStdout: true).trim()			
	}
      }
    }
  }
}
