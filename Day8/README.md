# Day 8

Lab - Kindly check if you have tkn client installed
```
tkn version
oc get crds | grep tekton
```

Expected output
![tekton](tekton1.png)

## Info - Tekton Jargons
<pre>
- Red Hat Pipeline operator installs Tekton Knative Serverless Pipeline Framework into openshift
- the operators also adds many Custom Resources like
  - Task
  - TaskRun
  - Pipeline
  - PipelineRun
  - PipelineResources
  - Catalog
  - Tekton Trigger
</pre>


## Info - What is a Step in Tekton Task?
<pre>
- Step is a Custom Resource added by Tekton in our openshift cluster using Custom Resource Definition(CRD)
- Each Step runs in a separate Container
- Steps can't be executed independed
- Steps always runs within a Tekton Task
</pre>

## Info - What is a Tekton Task?
<pre>
- Custom Resource added by Red Hat Openshift Pipeline operator using CRD
- Task can be executed independently outside a Tekton Pipeline
- Task supports two scopes
  - Project scope
  - Cluster wide
- Each task contains one or more Steps
- Examples
  - A Task can be used to clone source code from GitHub
  - A Task can build a container image, etc.,
</pre>
