pipeline {

    agent any

    stages {

        stage('Build') {

            steps {

                sh '''
                docker build -t odavies15/task1jenk
                '''

            }

        }

        stage('Push') {

            steps {

                sh '''
                docker push odavies15/task1jenk
                '''

            }

        }

        stage('Deploy') {

            steps {

                sh '''
                docker stop myimage
                docker rm myimage
                docker run -d -p 80:80 --name task1 odavies15/task1jenk
                '''

            }

        }

    }

}