pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh '''gradle build
gradle javadoc
'''
        archiveArtifacts 'build/libs/*.jar'
      }
    }
    stage('Mail Notification') {
      steps {
        mail(subject: 'Build Failed', body: 'This Build is failed', bcc: 'fm_zerrouk@esi.dz')
      }
    }
    stage('Code Analysis') {
      parallel {
        stage('Code Analysis') {
          
          steps {
    withSonarQubeEnv('sonarqube') {
      sh 'sonar-scanner'
                                            }
            
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
      steps {
        sh 'gradle uploadArchives'
      }
    }
  }
}
