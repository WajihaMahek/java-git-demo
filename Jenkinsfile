pipeline {
  agent any
  stages {
    stage('Compile') {
      steps {
        echo "Compiling code..."
        sh 'mvn -B -DskipTests clean package'
      }
    }
    stage('Code Review') {
      steps {
        echo "Running code review checks..."
        sh 'mvn checkstyle:check || true'
      }
    }
    stage('Unit Test') {
      steps {
        echo "Running unit tests..."
        sh 'mvn test'
      }
      post {
        always {
          junit 'target/surefire-reports/*.xml'
        }
      }
    }
    stage('Metric Check') {
      steps {
        echo "Generating code coverage..."
        sh 'mvn org.jacoco:jacoco-maven-plugin:prepare-agent test jacoco:report'
      }
    }
    stage('Package Check') {
      steps {
        echo "Archiving artifacts..."
        archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
      }
    }
    stage('Deploy') {
      steps {
        echo "Deploying application..."
        sh 'echo Deploying app here (replace with real deploy steps)'
      }
    }
  }
}
