pipeline{
    agent any
    stages{
        stage ("Build Docker Image"){
            steps{
                echo "Build Docker Image"
                bat "docker build -t app:v2 ."
            }
        }
        stage ("Docker Login"){
            steps{
                bat "docker login -u charithasree37 -p Krishna@09"
            }
        }
        stage("push Docker Iamge to Docker Hub"){
            steps {
                echo "push Docker Image to docker hub"
                bat "docker tag app:v2 charithasree37/cs1:last"
                bat "docker push charithasree37/cs1:last"


            }
        }
        stage("Deploy to Kubernetes"){
            steps{
                bat "kubectl apply -f deployment.yaml --validate=false"
                bat "kubectl apply -f service.yaml"
            }
        }
    }
    post{
        success{
            echo 'Pipeline completed scucessfull!'

        }
        failure{
            echo "Pipeline failed.Please check the logs."
        }
    }
}