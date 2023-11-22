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
                echo 'Deploying the artifact';
                sshagent(credentials: ['ec2-tomcat-ssh-id']) {
                    sh '''
                    [ -d ~/.ssh ] || mkdir ~/.ssh && chmod 0700 ~/.ssh
                    ssh-keyscan -t rsa,dsa ec2-13-235-0-125.ap-south-1.compute.amazonaws.com >> ~/.ssh/known_hosts
                    scp target/SimpleMavenWebAppProject-1.0-SNAPSHOT.war tomcat@ec2-13-235-0-125.ap-south-1.compute.amazonaws.com:/opt/tomcat/webapps
                    ssh ubuntu@ec2-13-235-0-125.ap-south-1.compute.amazonaws.com "sudo service tomcat restart"
                    '''
                }

            }
        }
    }
}