pipeline {
    agent any
    tools {
        maven 'Maven Default'
    }
    stages {
        stage('01 - Test'){
            steps {
                git url: 'https://github.com/prisoares/argentum-web'
                sh 'mvn clean test'
                cleanWs()
            }
        }
        stage('02 - Package') {
            steps {
                git url: 'https://github.com/prisoares/argentum-web'
                sh 'mvn package'
            }
        }
        stage('03 - Deploy') {
            environment {
                TOMCAT_CREDS = credentials('tomcat-credentials')
             
            }
            steps {
                sh 'curl -s --upload-file ${WORKSPACE}/target/argentum-web.war "http://${TOMCAT_CREDS_USR}:${TOMCAT_CREDS_PSW}@${TOMCAT_URL}:8080/manager/text/deploy?path=/argentum-web&update=true"'
            }
        }
    }
}
