# Day 7

## Info - Helm Overview
<pre>
- is a package manager for kubernetes and openshift
- helm will automatically find the dependency(order) in which the yaml files must be installed/deleted, etc.,
- through helm we can deploy/undeploy/upgrade our applications into Kubernetes/Openshift
- the packaged application is called chart
- we can package our custom applications as helm chart and then we can release to our customers
- our customer can then easily install our application using helm package manager
- helm also has marketplace, where you can download free/commerical helm charts and install them into our cluster
</pre>

## Lab - Creating a custom helm chart for our wordpress deployment and deploying wordpress chart into openshift

We need to first create the helm chart
```
cd ~/openshift-tekton-june2024
git pull
cd Day7/helm
helm create wordpress
cd wordpress/templates
rm -rf *
cd ../..
cp manifest-scripts/*.yml wordpress/templates
cp values.yaml wordpress
tree wordpress
```

We need to create the helm chart package
```
cd ~/openshift-tekton-june2024
git pull
cd Day7/helm

helm package wordpress
ls -l
```

We can install our custom wordpress helm chart as shown below
```
cd ~/openshift-tekton-june2024
git pull
cd Day7/helm

helm install wordpress wordpress-0.1.0.tgz
helm list
```

You can check if the application is deployed in your project namespace from the webconsole

Once you are done, you may delete it either from webconsole helm page or from cli
```
helm list
helm uninstall wp
```

Your end-user who are using the helm chart that you packaged can configure their specific values in the values.yaml file 
```
helm show values wordpress-0.1.0.tgz 
```

Once they found the values which can be customized using the above command, they can create a values.yaml with their customized values
```
helm install wp -f values.yaml wordpress-0.1.0.tgz
```


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


