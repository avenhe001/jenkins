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
	  script{
		string slackname = sh(script: """ aws cloudformation list-stacks --query 'StackSummaries[*]['StackName']' --stack-status-filter CREATE_COMPLETE --region 'ap-southeast-1' --output text""",returnStdout: true).trim()
		echo slackname
		if ( slackname == 'vpctestforaven' ){
		  sh "aws cloudformation update-stack --stack-name vpctestforaven --template-body file://VPC/vpc-all-with-no-configuration-parameters.json --region 'ap-southeast-1'"
		}
		else {
		  sh "aws cloudformation create-stack --stack-name vpctestforaven --template-body file://VPC/vpc-all-with-no-configuration-parameters.json --region 'ap-southeast-1'"
		}
	  }
	}
      }
    }
  }
}
