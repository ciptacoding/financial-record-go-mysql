pipeline {
    agent { label 'dev' }

    stages {
        stage('Pull SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/ciptacoding/financial-record-go-mysql.git'
            }
        }
        
        stage('Build') {
            steps {
                sh'''
                cd app
                go mod tidy
                '''
            }
        }
        
        stage('Code Review') {
            steps {
                sh'''
                cd app
                sonar-scanner   -Dsonar.projectKey=app-amar   -Dsonar.sources=.   -Dsonar.host.url=http://172.23.10.13:9000   -Dsonar.token=sqp_32f5a52e3eac1c778032e92e67f28f2113b97387
                '''
            }
        }
        
        stage('Deploy') {
            steps {
                sh'''
                docker compose up --build -d
                '''
            }
        }
        
        stage('Backup') {
            steps {
                 sh 'docker compose push' 
            }
        }
    }
}