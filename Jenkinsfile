pipeline{
    agent any

    tools {
         maven 'maven'
         jdk 'openjdk-11'
    }

    stages{
        stage('Compile') {
            steps {
                sh 'mvn compile'
            }
        }

        stage('Code Review') {
            steps {
                echo 'Code review is done'
            }
        }

        stage('Unit Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the artifact'
                // Add steps for deployment here
            }
        }
    }
}