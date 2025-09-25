pipeline {
    agent any
    environment {
        OPENFIRE_TAG =  'v5.0.1'
        SINTSE_TAG = 'v9.9.9'
    }
    stages {
        stage('build-server') {
            steps {
                sh "/usr/local/bin/docker pull ghcr.io/igniterealtime/openfire:$OPENFIRE_TAG"
            }
        }
        stage('run-server') {
            steps {
                sh "/usr/local/bin/docker run -d \
                    --name openfire-server \
                    -p 5222:5222 \
                    -p 5223:5223 \
                    -p 7070:7070 \
                    -p 9090:9090 \
                    -p 9091:9091 \
                    ghcr.io/igniterealtime/openfire:$OPENFIRE_TAG \
                    -demoboot"
                sh '/usr/local/bin/docker pull wait4x/wait4x:latest'
                sh '/usr/local/bin/docker run --rm wait4x/wait4x:latest http http://host.docker.internal:9090'
                sh '/usr/local/bin/docker run --rm wait4x/wait4x:latest tcp host.docker.internal:7070'
            }
        }
        stage('test-server') {
            steps {
                sh "/usr/local/bin/docker pull ghcr.io/xmpp-interop-testing/xmpp_interop_tests:$SINTSE_TAG"
                sh "/usr/local/bin/docker run \
                        -v ./xmpplogs:/logs \
                        ghcr.io/xmpp-interop-testing/xmpp_interop_tests:$SINTSE_TAG \
                        --domain=example.org \
                        --host=host.docker.internal \
                        --timeout=5000 \
                        --adminAccountUsername=admin \
                        --adminAccountPassword=admin \
                        --enabledTests='VCardTempIntegrationTest'"
            }
        }
    }
    post {
        always {
            sh '/usr/local/bin/docker stop openfire-server || true'
            sh '/usr/local/bin/docker rm openfire-server || true'
            cleanWs()
        }
    }
}
