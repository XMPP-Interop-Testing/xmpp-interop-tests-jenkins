# xmpp-interop-tests-jenkins
Run XMPP Interop tests on an XMPP server implementation using Jenkins

## Notes

Can run a Jenkinsfile via Jenkinsfile-Runner with

```
 docker run --rm -v $(pwd):/workspace ghcr.io/jenkinsci/jenkinsfile-runner:latest
 ```

 But it's stuck on Java 11, so won't run Openfire 5

 It's also not built on Docker-in-Docker, so would can't run an Openfire container.

 But we could write a GHA job to start Openfire and just use the runner for the tests

 Or we could build our own DinD image from this - plenty of folks seem to have

 Or we can wait for Java 17 - that seems to be active right now - or even help with it. <https://github.com/jenkinsci/jenkinsfile-runner/pull/733>

 I tried CloudBees, but that's not going anywhere - that's not hosted Jenkins. Whatever we're doing is going to need start in another CI system (assuming we don't want to host our own permanent Jenkins infrastructure)
