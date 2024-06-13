# Day 3

## Lab - Building your custom Docker Image
```
cd ~/openshift-tekton-june2024
git pull
cd Day3/spring-ms
docker build -t hello:1.0 .
docker images
```

## Lab - Rolling update 
<pre>
- Assume you have your microservice version 2.0 in the openshift cluster and you wish to upgrade to version 3.0 without any downtime
- in such cases, you can go for rolling update
</pre>

Let's first deploy the sample spring-boot microservice as shown below
```
oc new-project jegan
oc create deployment hello --image=tektutor/hello:2.0 --replicas=3
oc get deploy,rs,po
```

Now you may check the version of container our hello pod are using as shown below
```
oc get pod/hello-5c886db5d8-72hln -o yaml | grep tektutor/hello
```

Now, let's upgrade our microservice version from 2.0 to 3.0 as shown below
```
oc set image deploy/hello hello=hello hello=tektutor/hello:3.0
```

Now you may chek the version of the container our hello pods are using as shown below
```
oc get pod/hello-779467b6bf-g8mgm -o yaml | grep tektutor/hello
```

You can check the rolling update status as shown below
```
oc rollout status deploy/hello
oc rollout history deploy/hello
```

You wish to rollback to previous version of image
```
oc rollout undo deploy/hello
```
