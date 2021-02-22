podTemplate(label: 'mypod', containers: [
    containerTemplate(name: 'git', image: 'alpine/git', ttyEnabled: true, command: 'cat'),
    containerTemplate(name: 'maven', image: 'maven:3.3.9-jdk-8-alpine', command: 'cat', ttyEnabled: true),
    containerTemplate(name: 'docker', image: 'docker', command: 'cat', ttyEnabled: true),
    containerTemplate(name: 'dockercompose', image: 'docker/compose', command: 'cat', ttyEnabled: true)
  ],
  volumes: [
    hostPathVolume(mountPath: '/var/run/docker.sock', hostPath: '/var/run/docker.sock'),
  ]
  ) {
    node('mypod') {
        stage('Clone repository') {
            container('git') {
                sh 'whoami'
                sh 'hostname -i'
                sh 'git clone https://github.com/soumodeep46/cont.git'
            }
        }
        stage('build image'){
            container('docker'){
                dir('cont/'){
                    sh 'docker images'
                    sh 'ls'
                    container('dockercompose'){
                        sh 'docker-compose build'
                        sh 'docker tag cont_web cont_web_1:1.0.4'
                        sh 'docker images'
                        sh 'docker-compose up'
                    }
                    sh 'docker images'
                }
            }
        }
    }
}
