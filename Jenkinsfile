def projectName = 'rightstuff-176212';
def imageName = 'gcr.io/rightstuff-176212/jenkins-slave:docker.master'

podTemplate(cloud: 'local cluster', label: 'docker',
    containers: [containerTemplate(name: 'docker', image: imageName, command: 'cat', ttyEnabled: true, alwaysPullImage: true) ],
    volumes: [hostPathVolume(hostPath: '/var/run/docker.sock', mountPath: '/var/run/docker.sock')]) {
    node('docker') {
        container('docker') {
            checkout scm

            ansiColor('xterm') {
                stage('Build docker image') {
                    def branchImageTag = "gcr.io/${projectName}/jenkins-slave:docker.${env.BRANCH_NAME}"
                    def imageTag = "${branchImageTag}.${env.BUILD_NUMBER}"

                    env.DOCKER_API_VERSION = '1.23'
                    sh "DOCKER_API_VERSION=1.23 docker build -t ${imageTag}  ./docker"
                    sh "DOCKER_API_VERSION=1.23 docker tag ${imageTag} ${branchImageTag}"
                    sh "DOCKER_API_VERSION=1.23 gcloud docker -- push ${imageTag}"
                    sh "DOCKER_API_VERSION=1.23 gcloud docker -- push ${branchImageTag}"
                }

                stage('Build node image') {
                    def branchImageTag = "gcr.io/${projectName}/jenkins-slave:node.${env.BRANCH_NAME}"
                    def imageTag = "${branchImageTag}.${env.BUILD_NUMBER}"

                    env.DOCKER_API_VERSION = '1.23'
                    sh "DOCKER_API_VERSION=1.23 docker build -t ${imageTag} ./node"
                    sh "DOCKER_API_VERSION=1.23 docker tag ${imageTag} ${branchImageTag}"
                    sh "DOCKER_API_VERSION=1.23 gcloud docker -- push ${imageTag}"
                    sh "DOCKER_API_VERSION=1.23 gcloud docker -- push ${branchImageTag}"
                }
            }
        }
    }
}