pipeline {

    agent any
    environment {
        YOUR_NAME = credentials("YOUR_NAME")
    }
    stages {

        stage('Build') {

            steps {

                sh '''
                docker build -t odavies15/task1jenk .
                docker build -t odavies15/task1-nginx nginx
                '''

            }

        }

        stage('Push') {

            steps {

                sh '''
                docker push odavies15/task1jenk
                docker push odavies15/task1-nginx
                '''

            }

        }

        stage('Deploy') {

            steps {

                sh '''
                ssh jenkins@oli-deploy <<EOF
                docker stop nginx && echo "Stopped nginx" || echo "nginx is not running"
                docker rm nginx && echo "removed nginx" || echo "nginx does not exist"
                docker stop flask-app1 && echo "Stopped flask-app1" || echo "flask-app1 is not running"
                docker rm flask-app1 && echo "removed flask-app1" || echo "flask-app1 does not exist"
                docker stop flask-app2 && echo "Stopped flask-app2" || echo "flask-app2 is not running"
                docker rm flask-app2 && echo "removed flask-app2" || echo "flask-app2 does not exist"
                docker stop flask-app3 && echo "Stopped flask-app3" || echo "flask-app3 is not running"
                docker rm flask-app3 && echo "removed flask-app3" || echo "flask-app3 does not exist"
                docker network rm task1-net && echo "removed network" || echo "network already removed"
                docker network create task1-net
                docker run -d --name flask-app1 --network task1-net odavies15/task1jenk
                docker run -d --name flask-app2 --network task1-net odavies15/task1jenk
                docker run -d --name flask-app3 --network task1-net odavies15/task1jenk
                docker run -d --name nginx --network task1-net -p 80:80 odavies15/task1-nginx
                '''

            }

        }

    }

}