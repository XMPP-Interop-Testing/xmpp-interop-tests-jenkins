pipeline {
    agent any
    environment {
        OPENFIRE_VERSION_DOTS =  "5.0.1"
        OPENFIRE_VERSION_DASHES = "5_0_1"
        SINTSE_VERSION = "v1.6.1"
    }
    stages {
        stage('build-server') {
            steps {
                sh 'curl -L "https://github.com/igniterealtime/Openfire/releases/download/v$OPENFIRE_VERSION_DOTS/openfire_$OPENFIRE_VERSION_DASHES.tar.gz" -o openfire.tar.gz'
                sh 'mkdir openfire'
                sh 'tar -xzf openfire.tar.gz'
            }
        }
        stage('run-server') {
            steps {
                sh './scripts/startCIServer.sh -h "example.org" -b "./openfire"'
            }
        }
        stage('test-server') {
            steps {
                sh 'docker run \
                        --network=host \
                        -v "$(pwd)"/xmpplogs:/logs \
                        ghcr.io/xmpp-interop-testing/xmpp_interop_tests:$SINTSE_VERSION \
                        --domain=example.org \
                        --host=127.0.0.1 \
                        --timeout=5000 \
                        --adminAccountUsername=admin \
                        --adminAccountPassword=admin \
                        --enabledTests="VCardTempIntegrationTest"'
            }
        }
    }
}
