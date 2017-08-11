podTemplate(cloud: 'local cluster', label: 'jenkins-slave-k8s', containers: [
    containerTemplate(
        name: 'jenkins-slave',
        image: 'jenkinsci/slave:3.7-1',
        ttyEnabled: true, 
        command: 'cat',
        volumes: [
            hostPathVolume(hostPath: '/var/run/docker.sock', mountPath: '/var/run/docker.sock'),
            hostPathVolume(hostPath: '/usr/bin/docker', mountPath: '/usr/bin/docker')
        ]
    )
]) {
    node('jenkins-slave-k8s') {
        checkout scm
        
        stage('Setup Environment') {
            // Install tools
            sh 'curl -fsSL https://get.docker.com/ | sh'
        }

        stage('Build Node Docker') {
            sh 'docker build -t rightstuff-brewing/jenkins-slave:node ./node'
        }
    }
}