def DIST_ARCHIVE = "dist.${env.BUILD_NUMBER}"
def S3_BUCKET = 'source-bucket-demo14'

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
     
     stage('Unit Test') {
            sh 'ng test'
     }
    // stage("Copy") {
    //     sh "cp -a /var/lib/jenkins/workspace/angular-pipeline/dist/jenkins-test/. /var/www/jenkins_test/html/"
    // }
   stage('Archive') {
            sh "cd dist && zip -r ../${DIST_ARCHIVE}.zip . && cd .."
            archiveArtifacts artifacts: "${DIST_ARCHIVE}.zip", fingerprint: true
        }
}
  

