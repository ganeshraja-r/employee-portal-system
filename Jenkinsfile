pipeline {
    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("employee-app-${env.BRANCH_NAME}")
                }
            }
        }

        stage('Deploy Main Branch') {

            when {
                branch 'main'
            }

            steps {

                sh '''
                docker rm -f employee-main || true

                docker run -d \
                --name employee-main \
                -p 3000:80 \
                employee-app-main
                '''
            }
        }

        stage('Deploy Develop Branch') {

            when {
                branch 'develop'
            }

            steps {

                sh '''
                docker rm -f employee-develop || true

                docker run -d \
                --name employee-develop \
                -p 4000:80 \
                employee-app-develop
                '''
            }
        }
    }
}
