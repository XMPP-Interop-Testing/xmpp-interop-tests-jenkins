# XMPP Interop Tests in Jenkins

This repository contains a Jenkinsfile with an example of how to run the [XMPP Interop](https://xmpp-interop-testing.github.io/) tests (developed [here](https://github.com/XMPP-Interop-Testing/smack-sint-server-extensions)) against a server built in Jenkins.

This is largely just a Groovy implementation of the XMPP Interop Tests [instructions on Docker](https://xmpp-interop-testing.github.io/documentation/docker).

## Running the tests

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
