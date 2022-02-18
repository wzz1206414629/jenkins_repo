pipeline {
     agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2 --privileged'
        }
    }
    stages {

        stage('checkout code') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/${branch}']], extensions: [], userRemoteConfigs: [[credentialsId: 'e47ec2c9-de46-44fd-9bf0-4fd173bc54cb', url: 'git@github.com:wzz1206414629/jenkins_repo.git']]])
                echo 'pull code success'
            }
        }

        stage('Build') {
            steps {
                echo 'start package'
                sh 'mvn -B -DskipTests clean package'
                echo 'maven package jar success'
            }

            steps {
                echo 'docker build image'
                sh 'ls'
                sh 'docker build -t app:1.0 .'
            }
        }

        stage('Run app') {
            steps {
                sh 'docker run -d -p 8080:8080 app:1.0'
            }
        }
    }
}
