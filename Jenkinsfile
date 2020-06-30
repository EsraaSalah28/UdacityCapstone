pipeline {
    agent any
   

    stages {
        stage('Test') {
            steps {
               sh "python3 PythonApp/tests/test.py"
            }
        }

        stage('build') {
            steps {
                sh "docker build --tag=python_app ."
            }
        }

        stage('push image to docker hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: '281996', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')])
                  sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                  sh 'docker tag python_app 281996/python_app:dev'
                  sh "docker push 281996/python_app"
                }
            } 
        }
}
