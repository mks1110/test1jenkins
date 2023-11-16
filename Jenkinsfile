pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh '''
                docker build -t mks1011/task1jenk .
                docker build -t mks1011/task1-nginx nginx
                '''
            }

        }
        stage('Push') {
            steps {
                sh '''
                docker push mks1011/task1jenk
                docker push mks1011/task1-nginx
                '''
            }

        }
        stage('Deploy') {
            steps {
                sh '''
                ssh jenkins@michaela2-deploy <<EOF
                docker network rm task1-net && echo "removed network" || echo "network already removed"
                docker network create task1-net
                docker stop nginx && echo "stopped nginx" || echo "nginx is not running"
                docker rm nginx && echo "removed nginx" || echo "nginx does not exist"
                docker stop flask-app && echo "stopped flask-app" || echo "flask-app is not running"
                docker rm flask-app && echo "removed flask-app" || echo "flask-app does not exist"
                docker run -d --name flask-app --network task1-net mks1011/task1jenk
                docker run -d --name nginx --network task1-net -p 80:80 mks1011/task1-nginx
                '''
            }

        }

    }

}