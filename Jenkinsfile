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
                //sh 'cd ./tomcat/apache-tomcat-6.0.53-src/ && mvn test'
                //junit './tomcat/apache-tomcat-6.0.53-src/target/surefire-reports/*.xml'
            }
        }
        stage('Emma') {
            steps {
                echo 'Emma...'
                //sh 'cd ./tomcat/apache-tomcat-6.0.53-src/ && mvn emma:emma'
                //archiveArtifacts artifacts: 'tomcat/apache-tomcat-6.0.53-src/target/site/emma/index.html'
            }
        }

/*
        stage('Checkstyle'){
            steps {
                echo 'Checkstyle...'
                sh 'cd ./tomcat/apache-tomcat-6.0.53-src/ && mvn checkstyle:check > /var/lib/jenkins'
            }
        }
        */
        stage('Findbugs'){
            steps {
                echo 'Checkstyle...'
                sh 'cd ./tomcat/apache-tomcat-6.0.53-src/ && mvn clean findbugs:findbugs -xdocs -output ./target/findbugs.xml'
                archiveArtifacts artifacts: 'tomcat/apache-tomcat-6.0.53-src/target/site/'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying...'
            }
        }
    }
}
