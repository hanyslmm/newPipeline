pipeline {
     agent any
     stages {
         stage('Build') {
             steps {
<<<<<<< HEAD
                 sh 'echo "Hello Hany"'
=======
                 git pull
                 sh 'echo "Hello World"'
>>>>>>> ede8c63ad2f2743d0fb30f93c8c0c456ac612d14
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
                 aquaMicroscanner imageName: 'alpine:latest', notCompleted: 'exit 1', onDisallowed: 'fail'
              }
         }
         stage('Upload to AWS') {
              steps {
                  withAWS(region:'us-east-2',credentials:'aws-static') {
                  sh 'echo "Uploading content with AWS creds"'
                      s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file:'index.html', bucket:'hany-jenkinse')
                  }
              }
         }
     }
}
