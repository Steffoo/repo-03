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
        /*
        stage('Test') {
            steps {
                echo 'Testing..'
                //sh 'cd ./tomcat/apache-tomcat-6.0.53-src/ && mvn test'
                //junit './tomcat/apache-tomcat-6.0.53-src/target/surefire-reports/*.xml'
            }
        }
        */
        stage('Emma') {
            steps {
                echo 'Emma...'
                sh 'cd ./tomcat/apache-tomcat-6.0.53-src/ && mvn emma:emma'
                archiveArtifacts artifacts: 'tomcat/apache-tomcat-6.0.53-src/target/site/emma/index.html'
                archiveArtifacts artifacts: 'tomcat/apache-tomcat-6.0.53-src/target/site/emma/coverage.xml'
            }
        }
        /*
        stage('Checkstyle'){
            steps {
                echo 'Checkstyle...'
                sh 'cd ./tomcat/apache-tomcat-6.0.53-src/ && mvn checkstyle:check > /var/lib/jenkins'
            }
        }
        stage('Findbugs'){
            steps {
                echo 'Findbugs...'
                sh 'cd ./tomcat/apache-tomcat-6.0.53-src/ && mvn findbugs:findbugs'
            }
        }
        */
        stage('Deploy') {
            steps {
                echo 'Deploying...'
            }
        }
    }

    publishHTML(target: [
    allowMissing: false, 
    alwaysLinkToLastBuild: false,
    keepAll: true,
    reportDir: './repo-03_repo-03_master-CMDODME52PJDU2EPVQQD5P4QJKXG2H2PXX4ZRHWWBHBYLZICVSDQ/tomcat/apache-tomcat-6.0.53-src/target/site/emma',
    reportFiles: 'index.html',
    reportName: 'Emma Report',
    reportTitles: ''
    ])
}
