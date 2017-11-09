pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                cd /tomcat/apache-tomcat-6.0.53-src/ && mvn clean compile assmebly:single
                echo 'Building..'
            }
        }
        stage('Test') {
            steps {
                cd /tomcat/apache-tomcat-6.0.53-src/ && mvn test
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
