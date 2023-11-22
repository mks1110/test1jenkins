pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh '''
                docker build -t mks1011/task1jenk .
                '''
            }

        }
        stage('Push') {
            steps {
                sh '''
                docker push mks1011/task1jenk
                '''
            }

        }
        stage('Deploy') {
            steps {
                sh '''
                kubectl apply -f .
                sleep 60
                kubectl get services
                '''
            }

        }

    }

}