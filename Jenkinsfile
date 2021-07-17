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
	  
    stage(Submit Stack') {
      steps {
        withAWS(roleAccount:'327173749814', role:'cloudformation') {
		sh 'TEMP_CFT=$(aws cloudformation describe-stacks --stack-name vpctestforaven)'
		sh 'export TEMP_CFT'
		sh 'echo $TEMP_CFT'	
		sh  "aws cloudformation create-stack --stack-name vpctestforaven --template-body file://VPC/vpc-all-with-no-configuration-parameters.json --region 'ap-southeast-1'"		
	}
      }
    }	  
  }
}
