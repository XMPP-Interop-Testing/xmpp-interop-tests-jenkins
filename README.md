# XMPP Interop Tests in Jenkins

This repository contains a Jenkinsfile with an example of how to run the [XMPP Interop](https://xmpp-interop-testing.github.io/) tests (developed [here](https://github.com/XMPP-Interop-Testing/smack-sint-server-extensions)) against a server built in Jenkins.

This is largely just a Groovy implementation of the XMPP Interop Tests [instructions on Docker](https://xmpp-interop-testing.github.io/documentation/docker).

To test the Jenkinsfile, see [TESTING.md] which includes basic instructions on how to set up a very basic and incredibly non-prod instance of Jenkins, and to validate that the flow executes sucessfully.
