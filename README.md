pipeline {
    agent any

    tools {
        maven 'MAVEN-HOME'
    }

    stages {
        stage('git repo & clean') {
            steps {
                bat 'git clone https://github.com/GirijaSundari/Maven.git'
                bat 'mvn clean -f Maven/pom.xml'
            }
        }

        stage('install') {
            steps {
                bat 'mvn install -f Maven/pom.xml'
            }
        }

        stage('test') {
            steps {
                bat 'mvn test -f Maven/pom.xml'
            }
        }

        stage('package') {
            steps {
                bat 'mvn package -f Maven/pom.xml'
            }
        }
    }
}

...........................
FROM nginx:alpine

COPY index.html /usr/share/nginx/html/index.html
