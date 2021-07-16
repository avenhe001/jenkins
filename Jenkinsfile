pipeline {
    agent any
    stages {
        stage('Submit Stack') {
            steps {
            sh "aws cloudformation create-stack --stack-name s3testforaven --template-body file://S3/clf-stg-kakao-s3-bucket.json --region 'ap-southeast-1'"
              }
             }
            }
            }