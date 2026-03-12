pipeline {
    agent any
    tools {
      maven 'Maven 3.9.13'
    }
    stages {
        stage ('build') {
            steps {
              echo 'compiling....'
                sh 'mvn compile'
            }
        }
        
        stage ('test') {
            steps {
              echo 'testing....'
                sh 'mvn clean test'
            }
        }
        
        stage ('package') {
            steps {
              echo 'packaging....'
                sh 'mvn package -DskipTests'
            }
        }
    }
   post {
        always {
            echo 'This pipeline is completed.'
        }
    }
}
