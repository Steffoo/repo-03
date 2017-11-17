pipeline {
    agent any
    triggers {
      pollSCM('*/5 * * * *')
    }
    stages {
        stage('Clean') {
          steps {
            sh 'cd ./tomcat/apache-tomcat-6.0.53-src/ && mvn clean'
          }
        }
        stage('Build') {
            steps {
                sh 'cd ./tomcat/apache-tomcat-6.0.53-src/ && mvn compile assembly:single'
                archiveArtifacts artifacts: '**/target/*jar-with-dependencies.jar', fingerprint: true
            }
        }
        stage('Test') {
            steps {
                sh 'cd ./tomcat/apache-tomcat-6.0.53-src/ && mvn test'
                //junit './tomcat/apache-tomcat-6.0.53-src/target/surefire-reports/*.xml'
            }
        }
        stage('Emma') {
            steps {
                sh 'cd ./tomcat/apache-tomcat-6.0.53-src/ && mvn emma:emma'
              }
                post {
                  success {
                    // publish html
                    publishHTML target: [
                      allowMissing: false,
                      alwaysLinkToLastBuild: false,
                      keepAll: true,
                      reportDir: 'tomcat/apache-tomcat-6.0.53-src/target/site/emma',
                      reportFiles: 'index.html',
                      reportName: 'Emma Report',
                    ]
                  }
                }
        }
        stage('Checkstyle'){
            steps {
                sh 'cd ./tomcat/apache-tomcat-6.0.53-src/ && mvn checkstyle:checkstyle'
                sh 'cd ./tomcat/apache-tomcat-6.0.53-src/ && mvn site checkstyle:checkstyle'
            }
            post {
              success {
                archiveArtifacts artifacts: '**/target/checkstyle-result.xml', fingerprint: true
                //checkstyle pattern: 'tomcat/apache-tomcat-6.0.53-src/target/checkstyle-result.xml'
                sh 'cd tomcat/apache-tomcat-6.0.53-src/target && zip -r site.zip site/'
                archiveArtifacts artifacts: '**/target/site.zip', fingerprint: true
              }
            }
        }
        stage('Findbugs'){
            steps {
                sh 'cd ./tomcat/apache-tomcat-6.0.53-src/ && mvn findbugs:findbugs'
            }
            post {
              success {
                findbugs pattern: 'tomcat/apache-tomcat-6.0.53-src/target/findbugsXml.xml'
              }
            }
        }
        stage('Deploy') {
            steps {
              sh 'cd ./tomcat/apache-tomcat-6.0.53-src/ && mvn assembly:single'
            }
            post{
              success{
                archiveArtifacts artifacts: '**/target/*jar-with-dependencies.jar', fingerprint: true
              }
            }
        }
    }
}
