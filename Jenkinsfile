def dtrVpnAddress = "vpn.corp-us-east-1.aws.dckr.io"
def ucpBundle = [file(credentialsId: "ucp-bundle", variable: 'UCP')]
def slackString = [string(credentialsId: 'slack-docs-webhook', variable: 'slack')]
def reg = [credentialsId: 'csebuildbot', url: 'https://index.docker.io/v1/']

pipeline {
  agent none
  options {
    timeout(time: 1, unit: 'HOURS') 
  }
  stages {
    stage( 'docs-private' ) {
      agent {
        label 'ubuntu-1604-aufs-stable'
      }
      steps {
          sh 'printenv'
      }
      // stages {
      //   stage( 'build and push image' ) {
      //     when {
      //       branch 'master'
      //     }
      //     steps {
      //       withDockerRegistry(reg) {
      //         sh """
      //           docker image build --tag docs/docs-private:build-${env.BUILD_NUMBER} . && \
      //           docker image push docs/docs-private:build-${env.BUILD_NUMBER}
      //         """
      //       }
      //     }
      //   }
      //   stage( 'update service' ) {
      //     when {
      //       branch 'master'
      //     }
      //     steps {
      //       withVpn(dtrVpnAddress) {
      //         withCredentials(ucpBundle) {
      //           sh 'unzip -o $UCP' 
      //         }
      //         withDockerRegistry(reg) {
      //           sh """
      //             export DOCKER_TLS_VERIFY=1
      //             export COMPOSE_TLS_VERSION=TLSv1_2
      //             export DOCKER_CERT_PATH=${WORKSPACE}/ucp-bundle-success_bot
      //             export DOCKER_HOST=tcp://ucp.corp-us-east-1.aws.dckr.io:443
      //             docker service update --detach=false --force --image docs/docs-private:build-${env.BUILD_NUMBER} docs-beta-docker-com_docs --with-registry-auth
      //           """
      //         }
      //       }
      //     }
      //   }
      // }
    }
  }
}
