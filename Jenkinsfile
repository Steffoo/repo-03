pipeline {
    agent any
    triggers {
      pollSCM('*/5 * * * *')
    }

    stages {
        stage('Build') {
            steps {
                sh 'cd ./tomcat/apache-tomcat-6.0.53-src/ && mvn clean compile assembly:single'
                archiveArtifacts artifacts: '**/target/*jar-with-dependencies.jar', fingerprint: true
                echo 'Building..'
            }
        }
        stage('Test') {
            steps {
                sh 'cd ./tomcat/apache-tomcat-6.0.53-src/ && mvn test'
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
                echo 'Just a test...'
            }
        }
    }
}
