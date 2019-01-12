pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        bat 'gradle build'
        bat 'gradle javadoc'
        archiveArtifacts 'C:\\Users\\madjda\\Desktop\\ESI\\2CS\\OuTils\\Tp6\\MatrixRelease\\Matrix_v_1.0\\API\\tp6.jar'
        archiveArtifacts 'C:\\Users\\madjda\\Desktop\\ESI\\2CS\\OuTils\\Tp6\\MatrixRelease\\Matrix_v_1.0\\documentation'
      }
    }
  }
}