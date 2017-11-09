pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                mvn clean compile assmebly:single
                echo 'Building..'
            }
        }
        stage('Test') {
            steps {
                mvn test
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
