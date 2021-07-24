pipeline {
    agent any
    environment {
        PATH = "/usr/share/maven/bin:$PATH"
    }
    stages {
        stage("clone code"){
            steps{
               git credentialsId: 'vprasadk111git', url: 'https://github.com/vprasadk111/hello-world.git'
            }
        }
        stage("build code"){
            steps{
              sh "mvn clean install"
            }
        }
        stage("deploy"){
            steps{
              sshagent(['deployuser']) {
                 sh "scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/maven-project/webapp/target/webapp.war ec2-user@172.31.59.159:/tmp/TOMCAT/apache-tomcat-9.0.50/webapps/"
                 
                }
            }
        }
    }
}
