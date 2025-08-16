pipeline {
  agent any
  stages {
    stage('Compile') {
      steps {
        echo "Compiling code..."
        bat 'mvn -B -DskipTests clean package'
      }
    }
    stage('Code Review') {
      steps {
        echo "Running code review checks..."
        bat 'mvn checkstyle:check || true'
      }
    }
    stage('Unit Test') {
      steps {
        echo "Running unit tests..."
        bat 'mvn test'
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
        bat 'mvn org.jacoco:jacoco-maven-plugin:prepare-agent test jacoco:report'
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
        bat 'echo Deploying app here (replace with real deploy steps)'
      }
    }
  }
}
