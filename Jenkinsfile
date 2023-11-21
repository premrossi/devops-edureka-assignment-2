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
                sshagent(['ec2-tomcat-ssh-id']) {
                    sh '''
                    scp target/SimpleMavenWebAppProject-1.0-SNAPSHOT.war ubuntu@ec2-13-235-0-125.ap-south-1.compute.amazonaws.com:/opt/tomcat/webapps
                    ssh ubuntu@ec2-13-235-0-125.ap-south-1.compute.amazonaws.com "sudo service tomcat restart"
                    '''
                }

            }
        }
    }
}