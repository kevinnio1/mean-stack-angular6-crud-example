def docker_hub_username = 'depauna'

def img_group_name = 'jenkins'
def img_name = 'book-store'
def img_tag = 'stable'

def icp_dev_registry = 'mycluster.icp:8500'

pipeline {
    agent { label 'master' }
    stages {
        stage('Built image') {
            steps {
                sh "sudo docker build . -t ${docker_hub_username}/${img_name}:${img_tag}"
            }
        }
        stage('Push image to Docker Hub') {
            steps {
                sh "sudo docker push ${docker_hub_username}/${img_name}:${img_tag}"
            }
        }
        stage('Tag and push image for local ICP cluster') {
            steps {
                sh "sudo docker tag ${docker_hub_username}/${img_name}:${img_tag} ${icp_dev_registry}/${img_group_name}/${img_name}:${img_tag}"
                sh "sudo docker push ${icp_dev_registry}/${img_group_name}/${img_name}:${img_tag}"
            }
        }
    }
}
