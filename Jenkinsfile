pipeline {

  agent any
  
  environment{
  ANYPOINT_CREDS =credentials('ANYPOINT_CREDENTIALS')
  }
  stages {
    stage('Build') {
      steps {
            bat 'mvn -B -U -e -V clean -DskipTests package'
      }
    }

    stage('Test') {
      steps {
          echo "******************MUNIT TEST CASE EXECUTION******************"
      }
    }

    stage('Deployment') {
    environment{
    CLIENT_ID = credentials('DEV_CLIENT_ID')
    CLIENT_SECRET = credentials('DEV_CLIENT_SECRET')
    }
      
      steps {
            bat 'mvn -U -V -e -B -DskipTests deploy -Pdev -DmuleDeploy -Dusername="%ANYPOINT_CREDS_USR%" -Dpassword="%ANYPOINT_CREDS_PSW%" -Danypoint.platform.client_id="%CLIENT_ID%" -Danypoint.platform.client_secret="%CLIENT_SECRET%"'
      }
    }
  }
   post {
        always {
           emailext body: 'Test Message',
    recipientProviders: [developers(), requestor()],
    subject: 'Test Subject',
    to: 'sidhanth488@gmail.com'
        }
    }
}
