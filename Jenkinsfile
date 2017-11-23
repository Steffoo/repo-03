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
                sh 'cd ./tomcat/apache-tomcat-6.0.53-src/ && mvn compile'
            }
        }
        stage('Test') {
            steps {
                sh 'cd ./tomcat/apache-tomcat-6.0.53-src/ && mvn test'
            }
        }
        stage('Reports') {
          steps{
            sh 'cd ./tomcat/apache-tomcat-6.0.53-src/ && mvn emma:emma findbugs:findbugs checkstyle:checkstyle -Dcheckstyle.config.location="${WORKSPACE}/tomcat/apache-tomcat-6.0.53-src/checkstyle.xml"'
            junit 'tomcat/apache-tomcat-6.0.53-src/target/surefire-reports/*.xml'
          }
          post {
            success {
              //Publish emma.html
              publishHTML target: [
                allowMissing: false,
                alwaysLinkToLastBuild: false,
                keepAll: true,
                reportDir: 'tomcat/apache-tomcat-6.0.53-src/target/site/emma',
                reportFiles: 'index.html',
                reportName: 'Emma Report',
              ]

              //Publish FindBugs
              findbugs pattern: 'tomcat/apache-tomcat-6.0.53-src/target/findbugsXml.xml'

              //Publish checkstyle
              checkstyle pattern: 'tomcat/apache-tomcat-6.0.53-src/target/checkstyle-result.xml', unstableTotalAll:'80000'
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
