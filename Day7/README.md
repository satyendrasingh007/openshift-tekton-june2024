# Day 7

## What is Continuous Integration(CI)?
<pre>
- SCRUM Daily stand-up meeting is a fail-fast meeting
- SCRUM Daily stand-up meeting is an inspect and adapt meeting
- similar to SCRUM daily stand-up, the equivalent engineering process is the Continuous Integration
- the source code has to integrated several times a day
- for the CI to work effectively, the automated build should involve automated test cases
- the team should have a culture, where build failures due to test case failure are treated as a good thing, and the management appreciates when such builds are broken
- build failure is the feedback your CI gives us, it found a bug during the early stage of development
- in CI builds, we need to automate builds along with unit and integration testing
</pre>

## What is Continuous Deployment(CD)?
<pre>
- the developer CI certified application binaries will be automatically deployed into QA env for further testing (automated and manual)
- once the automated QA test passes, the binaries is qa certified is ready for production

</pre>

## What is Continuous Delivery(CD)?
<pre>
- QA Certified binaries can be delivered automatically to the customer's environment
- the customer's environment could be pre-prod environment, where the customer will test manually and with automated test cases, if they find it good to go live, they make a call on when the product will be made live
</pre>

## DevOps Overview
<pre>
- whatever technical work we deliver, we need to look for ways to convert them into source code
- openshift declarative style follows devops philosopy correctly
- as the openshift manifest yaml files are source code, we can push them into version control
- for build & test automation (CI/CD), the foremost important thing is the source code should be available in version control
</pre>

## What are the CI/CD Build Servers available ?
<pre>
- Jenkins is open source developed by Josuke Kavaguchi (former Sun Microsystem employee )
- Hudson was the original Build server that was built by Josuke Kavaguchi and open source community
- after Oracle acquired Sun Microsystems, due to some conflict in idealogy the Hudson team created a branch/fork called Jenkins and they quit Oracle and they started developing Jenkins as an opensource product
- Jenkins has more 10000 word-wide opensource contributors
- the commercial variant of Jenkins is called Cloudbees

- TeamCity
- Bamboo
- CircleCI
- TFS
- Tekton
</pre>

## Info - Helm Overview
<pre>
- is a package manager for kubernetes and openshift
- through helm we can deploy/undeploy/upgrade our applications into Kubernetes/Openshift
- the packaged application is called chart
- we can package our custom applications as helm chart and then we can release to our customers
- our customer can then easily install our application using helm package manager
- helm also has marketplace, where you can download free/commerical helm charts and install them into our cluster
</pre>
