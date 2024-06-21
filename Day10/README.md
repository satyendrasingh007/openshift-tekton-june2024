# Day 10

## Reference
You may check my medium blog about CI/CD with Tekton on Openshift
<pre>
https://medium.com/tektutor/openshift-ci-cd-with-tekton-faa88ba45656  
</pre>

## Lab - Creating a declarative CI/CD Pipeline using TekTon knative Framework in Red Hat Openshift
```
cd ~/openshift-tekton-june2024
git pull
cd Day10
cat java-cicd-pipeline.yml

tkn task list
tkn taskrun list
tkn pipeline list
tkn pipelinerun list

oc apply -f java-cicd-pipeline.yml

tkn task list
tkn taskrun list
tkn pipeline list
tkn pipelinerun list

cat java-cicd-pipeline-run.yml
oc create -f java-cicd-pipeline-run.yml
tkn pipelinerun list --showlog
```

Expected output
![tekton](tekton1.png)
![tekton](tekton2.png)
![tekton](tekton3.png)
![tekton](tekton4.png)
![tekton](tekton5.png)
![tekton](tekton6.png)
![tekton](tekton7.png)
![tekton](tekton8.png)
![tekton](tekton9.png)
![tekton](tekton10.png)
![tekton](tekton11.png)

## Lab - Triggering Tekton Pipeline using GitHub polling
<pre>
- We need to install tekton-polling operator
- this helps triggering pipeline on local openshift setup
- In case of local openshift setup, GitHub won't be able to invoke the Openshift public route url, hence the only way to trigger pipeline is using the polling operator
</pre>

Let's install the polling operator
<pre>
oc apply -f https://github.com/bigkevmcd/tekton-polling-operator/releases/download/v0.4.0/release-v0.4.0.yaml  
</pre>

Let's delete the existing pipeline
```
cd ~/openshift-tekton-june2024
git pull
cd Day10
tkn pipeline delete --all
tkn pipelinerun delete --all
```

Let's create the pipeline and setup the github polling
```
cd ~/openshift-tekton-june2024
git pull
cd Day10
cd tekton-trigger-github-polling
oc apply -f java-cicd-pipeline.yml
oc apply -f github-trigger.yml
```

Expected output
![tekton](tekton12.png)
![tekton](tekton13.png)
![tekton](tekton14.png)


## Lab - TekTon Trigger (GitHub webhook similulation with curl)
```
cd ~/openshift-tekton-june2024
git pull
cd Day10/tekton-trigger-github-webhook
oc apply -f first-pipeline.yml
oc apply -f tekton-trigger.yml
```

Check if the event listener pod is running
```
oc get pod --field-selector=status.phase==Running
```
Find the service name
```
oc get el tektutor-trigger-listener -o=jsonpath='{.status.configuration.generatedName}'
```

List the service now
```
oc get service $(oc get el tektutor-trigger-listener -o=jsonpath'{.status.configuration.generatedName}')
```

Load the service name into an environment variable
```
SVC_NAME=$(oc get el tektutor-trigger-listener -o=jsonpath='{.status.configuration.generatedName}')
```

Let's create a route
```
oc create route edge ${SVC_NAME}-route --service=${SVC_NAME}
```

See if the route is created
```
oc get route ${SVC_NAME}-route
```

Let's us invoke the Trigger now ( this is how github webhook will notifiy for Tekton Pipeline )
```
HOOK_URL=https://$(oc get route ${SVC_NAME}-route -o=jsonpath='{.spec.host}')
curl --insecure --location --request POST ${HOOK_URL} --header 'Content-Type: application/json' --data-raw '{"name": "run-my-app", "run-it": "yes-please}'
```
