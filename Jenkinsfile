def DIST_ARCHIVE = "dist.${env.BUILD_NUMBER}"
def S3_BUCKET = 'source-bucket-demo14'
def AWS_DEFAULT_REGION = 'us-east-2'

node {
    stage('Checkout SCM') {
        git branch: 'main', url: 'https://github.com/KeerthanaPonnaiyan/jenkins-test.git'
    }

    stage('Install node modules') {
        sh "npm install"
    }

    // stage("Test") {
    //     sh "npm run test-headless"
    // }

    stage("Build") {
        sh "npm run build --prod"
    }
     
     // stage('Unit Test') {
     //        sh 'ng test'
     // }
  
   stage('Archive') {
            sh "cd dist && zip -r ../${DIST_ARCHIVE}.zip . && cd .."
            archiveArtifacts artifacts: "${DIST_ARCHIVE}.zip", fingerprint: true
        }
  
   stage('deploy') {
            sh "aws configure set region $AWS_DEFAULT_REGION" 
            sh "aws configure set aws_access_key_id $AWS_ACCESS_KEY_ID"  
            sh "aws configure set aws_secret_access_key $AWS_SECRET_ACCESS_KEY"
            sh "aws s3 cp src/index.html s3://source-bucket-demo14"
            // sh "aws s3 website s3://source-bucket-demo14/ --index-document index.html"
        }
    }
