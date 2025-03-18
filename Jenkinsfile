pipeline {
    agent any
    
    tools {
        maven 'maven'
    }
    
    stages {
        stage ("pull src") {
            steps {
                git 'https://github.com/PrashanthMJ21/Job-Portal-SpringBoot-api.git'
            }
        }
        
        stage ("build") {
            steps {
                sh 'mvn clean package'
            }
        }
        
        stage ("stop existing application") {
            steps {
                sh "pkill -f 'job-portal-0.0.1-SNAPSHOT.jar' || true"
            }
        }
        
        stage ("deploy app") {
            steps {
                sh 'sudo java -jar target/job-portal-0.0.1-SNAPSHOT.jar > /dev/null 2>&1 &'
            }
        }
    }
}
