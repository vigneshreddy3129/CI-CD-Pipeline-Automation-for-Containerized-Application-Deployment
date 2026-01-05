pipeline {
    agent any

    tools {
        maven 'Mvn'
        jdk 'Java-11'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/vigneshreddy3129/CICD-Pipeline-Automation-using-Jenkins-Tomcat.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn package'
            }
        }

        stage('tomcat-deploy') {
            steps {
                sh 'cp /var/lib/jenkins/workspace/tomcat-deploy/target/*.war  /opt/apache-tomcat-9.0.113/webapps/'
                
                
            }
        }
        stage("docker image"){
            steps {
                sh "docker build -f tomcat -t "tomcat:1" ."
                sh "docker run -d -p 8081:8080 tomcat:1"
            }
        }
    }
}
