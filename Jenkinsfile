pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        echo 'compiling....'
        sh 'mvn compile'
      }
    }

    stage('test') {
      steps {
        echo 'testing....'
        sh 'mvn clean test'
      }
    }

    stage('package') {
      parallel {
        stage('package') {
          steps {
            echo 'packaging....'
            sh 'mvn package -DskipTests'
          }
        }

        stage('publish image') {
          steps {
            script {
              docker.withRegistry('https://index.docker.io/v1/', 'dockerlogin') {
                def commitHash = env.GIT_COMMIT.take(7)
                def dockerImage = docker.build("ductuanbl2000/sysfoo:${commitHash}", "./")
                dockerImage.push()
                dockerImage.push("latest")
                dockerImage.push("dev")
              }
            }

          }
        }

      }
    }

  }
  tools {
    maven 'Maven 3.9.13'
  }
  post {
    always {
      echo 'This pipeline is completed.'
    }

  }
}