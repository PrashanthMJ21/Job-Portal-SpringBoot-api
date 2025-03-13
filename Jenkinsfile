
pipeline {
    agent any
    tools {
        maven 'maven'
    }
    stages {
        stage("Pull SCM") {
            steps {
                git branch:"master",url:"https://github.com/PrashanthMJ21/Job-Portal-SpringBoot-api.git"
            }
        }
        stage("Prepare build") {
            steps {
                sh "mvn clean package"
            }
        }
        stage("Build image and push to dockerhub") {
            steps {
                script {
                    try {
                        sh "docker rmi pmj41/webapp"
                    }
                    catch(err) {
                        echo err.getMessage()
                    }
                }
                sh '''  mv target/job-portal.war .
                        docker build -t pmj41/webapp .
                        docker login -u pmj41 -p $DOCKER_HUB TOKEN
                        docker push pmj41/webapp
                    '''
            }
        }
        stage("Run docker image") {
            steps {
                sh "docker pull -f pmj41/webapp"
                sh "docker run -it -d -p 8081:8080 --name marcos pmj41/webapp"
            }
        }
        
    }
}
