# XMPP Interop Tests in Jenkins

This repository contains a Jenkinsfile with an example of how to run the [XMPP Interop](https://xmpp-interop-testing.github.io/) tests (developed [here](https://github.com/XMPP-Interop-Testing/smack-sint-server-extensions)) against a server built in Jenkins.

This is largely just a Groovy implementation of the XMPP Interop Tests [instructions on Docker](https://xmpp-interop-testing.github.io/documentation/docker).

## Running the tests

### Usage

In a Jenkinsfile, invoke the XMPP interop tests container by whichever means and plugins you have available. There's no XMPP Interop Tests plugin for Jenkins to just act as a wrapper for these tests. With no plugins available, but Docker available on the Jenkins Agent, a simple invocation would look like this:

```
stage('test-server') {
            steps {
                sh "docker run \
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
```

Note that the logs director is mapped as a volume in order to capture output in the Jenkins workspace.

### Configuration

The docker container being run takes a number of optional arguments that can be enumerated via `docker run ghcr.io/xmpp-interop-testing/xmpp_interop_tests:latest --help`.

```bash
Usage:
    --domain=DOMAIN                       XMPP domain name of server under test. (default: example.org)
    --host=HOST                           IP address or DNS name of the XMPP service to run the tests on. (default: 127.0.0.1)
    --timeout=TIMEOUT                     Timeout in milliseconds for any XMPP action (default: 5000)
    --adminAccountUsername=ADMINUSERNAME  Admin username for the service, to create test users (if not using IBR / XEP-0077)
    --adminAccountUsername=ADMINPASSWORD  Admin password for the service, as above
    --disabledTests=DISABLEDTESTS         Comma-separated list of tests to skip, e.g. EntityCapsTest,SoftwareInfoIntegrationTest
    --disabledSpecifications=DISABLEDSPECIFICATIONS
    --enabledTests=ENABLEDTESTS           Comma-separated list of the only tests to run, e.g. EntityCapsTest,SoftwareInfoIntegrationTest
    --enabledSpecifications=ENABLEDSPECIFICATIONS
                                          Comma-separated list of the only specifications to run, e.g. XEP-0030,XEP-0199
    --help                                This help message
                                          Comma-separated list of specifications to skip, e.g. XEP-0030,XEP-0199
```

## Contributing

To test the Jenkinsfile for correctness, see [TESTING.md] which includes basic instructions on how to set up a very basic and incredibly non-prod instance of Jenkins, and to validate that the flow executes sucessfully.
