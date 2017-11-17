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
            }
            post {
              success {
                checkstyle pattern: 'tomcat/apache-tomcat-6.0.53-src/target/checkstyle-result.xml'
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
            }
        }
    }
}
