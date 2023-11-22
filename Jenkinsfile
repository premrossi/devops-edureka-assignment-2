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
                    ssh-keyscan -t rsa,dsa ec2-3-110-186-227.ap-south-1.compute.amazonaws.com >> ~/.ssh/known_hosts
                    scp target/prem-edureka-aws-devops-assignment-1.0.0.war ubuntu@ec2-3-110-186-227.ap-south-1.compute.amazonaws.com:~/prem-edureka-aws-devops-assignment-1.0.0.war
                    ssh ubuntu@ec2-3-110-186-227.ap-south-1.compute.amazonaws.com "sudo mv ~/prem-edureka-aws-devops-assignment-1.0.0.war /opt/tomcat/apache-tomcat-9.0.83/webapps && sudo service tomcat restart"
                    '''
                }
            }
        }
    }
}
