podTemplate(cloud: 'local cluster', label: 'docker',
    containers: [containerTemplate(name: 'docker', image: 'docker', command: 'cat', ttyEnabled: true) ],
    volumes: [hostPathVolume(hostPath: '/var/run/docker.sock', mountPath: '/var/run/docker.sock')]) {
    node('docker') {
        container('docker') {
            checkout scm

            sh 'DOCKER_API_VERSION=1.23 docker build -t rightstuff-brewing/jenkins-slave:node ./node'
        }
    }
}