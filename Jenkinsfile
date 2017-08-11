def projectName = 'rightstuff-176212';

podTemplate(cloud: 'local cluster', label: 'docker',
    containers: [containerTemplate(name: 'docker', image: 'docker', command: 'cat', ttyEnabled: true) ],
    volumes: [hostPathVolume(hostPath: '/var/run/docker.sock', mountPath: '/var/run/docker.sock')]) {
    node('docker') {
        container('docker') {
            checkout scm

            stage('Build docker image') {
                def imageTag = "gcr.io/${projectName}/jenkins-slave:docker.${env.BRANCH_NAME}.${env.BUILD_NUMBER}"
                sh "DOCKER_API_VERSION=1.23 docker build -t ${imageTag}  ./docker"
                sh "gcloud docker -- push ${imageName}"
            }

            stage('Build node image') {
                def branchImageTag = "gcr.io/${projectName}/jenkins-slave:node.${env.BRANCH_NAME}"
                def imageTag = "${branchImageTag}.${env.BUILD_NUMBER}"

                sh "DOCKER_API_VERSION=1.23 docker build -t ${imageTag} ./node"
                sh "gcloud docker -- push ${imageName}"
                sh "gcloud docker -- push ${branchImageTag}"
            }
        }
    }
}