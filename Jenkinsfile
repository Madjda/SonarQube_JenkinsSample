pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh '''gradle build
gradle javadoc
gradle jar
'''
        archiveArtifacts 'build/libs/*.jar'
        archiveArtifacts 'build/docs/javadoc/'
      }
    }
    stage('Mail Notification') {
      steps {
        mail(subject: 'Build Success', body: 'This Build is successful', bcc: 'fm_zerrouk@esi.dz')
      }
    }
    stage('Code Analysis') {
      parallel {
        stage('Code Analysis') {
          steps {
            withSonarQubeEnv('sonarqube') {
              sh 'sonar-scanner'
            }

            waitForQualityGate true
          }
        }
        stage('Test Reporting') {
          steps {
            jacoco()
          }
        }
      }
    }
    stage('Deployment') {
      
      when {
        not {
          changeRequest target: 'master'
        }

      }
      
      steps {
        
        sh 'gradle uploadArchives'
      }
    }
    stage('Slack Notification') {
      steps {
        slackSend(channel: 'gradle', message: 'project deployed')
      }
    }
  }
}
