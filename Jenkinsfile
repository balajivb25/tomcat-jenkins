pipeline {
    agent any
    tools {
        maven 'Maven3.9.9'   // configure in Jenkins global tools
        jdk 'JDK21'          // configure in Jenkins global tools
    }
    environment {
        TOMCAT_URL = 'http://your-server-ip:8080'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', credentialsId: 'github-creds', url: 'https://github.com/balajivb25/website-jenkins-project.git'
            }
        }
        stage('Build WAR') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Deploy to Tomcat') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'tomcat-creds', path: '', url: "${TOMCAT_URL}")], contextPath: 'website', war: 'target/website.war'
            }
        }
    }
}
