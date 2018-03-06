pipeline {
    agent any

    environment {
        AWS_ACCESS_KEY_ID     = credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
        DOCKER_ID_USER =  credentials('DOCKER_ID_USER')
        DOCKER_ID_PASSWORD = credentials('DOCKER_ID_PASSWORD')
    }
    
    stages {
        stage('Build') {
            steps {
                echo "Running building ${env.BUILD_ID} on ${env.JENKINS_URL}"
                echo "Key: ${AWS_ACCESS_KEY_ID} Access: ${AWS_SECRET_ACCESS_KEY}"
                sh 'echo ${DOCKER_ID_PASSWORD} | docker login -u ${DOCKER_ID_USER} --password-stdin'
                sh 'docker build -t "${DOCKER_ID_USER}/nginx-lua" .'
                sh 'docker push ${DOCKER_ID_USER}/nginx-lua'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..NO'
            }
        }
        stage('Deploy to prod') {
            steps {
                echo 'Deploying....'
                sh 'docker-machine create --driver amazonec2 --amazonec2-access-key ${AWS_ACCESS_KEY_ID}  --amazonec2-secret-key ${AWS_SECRET_ACCESS_KEY} --amazonec2-open-port 80    aws-sandbox'
                sh 'docker-machine env aws-sandbox'
                sh 'docker-machine ssh aws-sandbox "sudo docker run -d -p80:80 --name webserver rooty/nginx-lua"'
                sh 'docker-machine ip aws-sandbox'
            }
        }
    }
}
