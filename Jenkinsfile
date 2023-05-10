pipeline {
  agent any
  stages {
    stage('git scm update') {
      steps {
        git url: 'https://github.com/IaC-Source/echo-ip.git', branch: 'main'
      }
    }
    stage('docker build and push') {
      steps {
        sh '''
        docker build -t 192.168.1.10:8443/echo-ip .
        docker push 192.168.1.10:8443/echo-ip
        '''
      }
    }
    stage('deploy kubernetes') {
      steps {
        sh '''
        kubectl create deployment sungmook-prod --image=kangmook/sungmook:v1.0
        kubectl expose deployment sungmook-prod --type=LoadBalancer --port=8080 \
                                               --target-port=80 --name=sungmook-prod-svc
        '''
      }
    }
  }
}
