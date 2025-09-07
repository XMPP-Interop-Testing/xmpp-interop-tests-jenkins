# Testing the Jenkinsfile

First, install Jenkins

Linux: `sudo apt-get install jenkins && sudo systemctl start jenkins`
macOS: `brew install jenkins-lts && brew services start jenkins-lts`

Get the default password (should be 32 characters of hex, e.g. 6a1fd6bae42d402fa02e89257a7c061b)

```sh
cat .jenkins/secrets/initialAdminPassword
```

Then:

- Open http://localhost:8080 and put in the password
- Opt to install the recommended plugins. Then wait a while.
- Skip user creation and continue as Admin
- Confirm the Jenkins URL as http://localhost:8080
- Click Start using Jenkins 

Then:

- Create a job
- Call it XMPPTest. Pick the Pipeline type, and click OK
- Under Pipeline, set the Definition to `Pipeline script from SCM`
- Set the SCM to Git
- Set the Repository URL to `git@github.com:XMPP-Interop-Testing/xmpp-interop-tests-jenkins.git`
- Set the branch specifier: `*/main`
- Click Save

Finally:

- Click Build Now