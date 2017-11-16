pipeline {
    agent any
    triggers {
      pollSCM('*/5 * * * *')
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                sh 'cd ./tomcat/apache-tomcat-6.0.53-src/ && mvn clean compile assembly:single'
                archiveArtifacts artifacts: '**/target/*jar-with-dependencies.jar', fingerprint: true
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
                sh 'cd ./tomcat/apache-tomcat-6.0.53-src/ && mvn test'
              
            }
        }
        stage('Emma') {
            steps {
                echo 'Emma...'
                sh 'cd ./tomcat/apache-tomcat-6.0.53-src/ && mvn emma:emma'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
            }
        }
    }
}
