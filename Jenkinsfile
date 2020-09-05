pipeline {
     agent any
     stages {
         stage('Build') {
             steps {
                 sh 'echo "Hello Hany"'
                 sh '''
                     echo "Multiline shell steps works too"
                     ls -lah
                     pwd
                 '''
             }
         }
         stage('Lint HTML') {
              steps {
                  sh 'tidy -q -e index.html'
              }
         }
         stage('Security Scan') {
              steps {
                 aquaMicroscanner imageName: 'alpine:latest', notCompliesCmd: 'exit 1', onDisallowed: 'fail', outputFormat: 'html'
              }
         }
         stage('Upload to AWS') {
              steps {
                  withAWS(region:'us-east-2',credentials:'aws-static') {
                  sh 'echo "Uploading content with AWS creds"'
                      s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file:'index.html', bucket:'static-jenkins-pipeline')
                  }
              }
         }
     }
}
