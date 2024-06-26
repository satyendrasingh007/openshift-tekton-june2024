# Day 6

## Info - Openshift Service
<pre>
- represents a groups of load-balanced pods from the same deployment
- service will forward the call to any one of the Pod within a single deployment
</pre>  

## Info - What is Ingress?
<pre>
- routing/forwarding rules
- Ingress helps in forwarding the calls to multiple different services pointing to different deployments
- Ingress is not a service
- We can declaratively create ingress rules, which are retreived by Ingress Controller, which then configures the load balancer with the forwarding rules we listing in the ingress
- For Ingress to work, we need the below
  - Ingress ( rules )
  - Ingress Controller
  - Load Balancer
</pre>

## Info - What is Ingress Controller?
- Ingress Controller is Controller like Deployment Controller, ReplicaSet Controller
- Ingress Controller keeps an eye on every new Ingress created in any project namespace
- Ingress Controller monitors any change done to existing Ingress resources under any project namespace
- Ingress Controller also will monitor when Ingress is deleted in any project namespace
- Ingress Controller picks the rules we mentioned in the Ingress resource and configures the load balancer accordingly
- There are two popular ingress controllers
  - Nginx Ingress Controller
  - HAProxy Ingress Controller
- In our lab setup, we are using HAProxy Load Balancer, hence we need to use HAProxy Ingress Controller

## Info - Deployment vs DeploymentConfigs
<pre>
- In older version of Kubernetes, we had to use ReplicationController to deploy applications into Kubernetes/Openshift
- The Red Hat openshift team, at that time added DeploymentConfig to allow deploying application in the declarative style as the ReplicationController doesn't support deploying application in the declarative style
- Meanwhile, the Google Kubernetes team & community added Deployment and ReplicaSet resource as an alternate for ReplicationController
- Hence, in Openshift the Red Hat team deprecated the use of DeploymentConfig as Deployment and DeploymentConfig pretty does the same
- Kubernetes, deprecated the use of ReplicationController
- Hence, whenever we deploy new appplication we need choose Deployment over the DeploymentConfig as DeploymentConfig internally uses ReplicationController
</pre>


## Info - ReplicationController vs ReplicaSet
- ReplicationController support both Rolling update and Scale up/down, which violates Single Responsibility Principle
- New applications should consider using Deployment over the ReplicationController
- When we create deployment, it automatically creates K8s Deployment resource and K8s ReplicaSet resource
- K8s Deployment resource is managed by Deployment Controller
- K8s ReplicaSet resource is managed by ReplicaSet Controller
- Deployment Controller supports rolling update
- ReplicaSet controller support scale up/down
- Hence, we should not use ReplicationController any more though it is there for backward compatibilty purpose
  
## Info - NodePort vs Route
<pre>
- NodePort is an external service
- It is a K8s features, which is also supported in openshift
- Kubernetes/Openshift reserve ports in range 30000-32767 for the purpose of NodePorts
- For each, NodePort service we create one of the ports from the above range will be alloted for the service
- the chose nodeport is opened in all the nodes for the nodeport service
- if we create 100 nodeport services, we end up opening 100 firewall ports on all the nodes, which is a security concern
- also nodeport service is not end-user friendly or developer friendly as they are accessed via node hostname/ip address, ideally the end-user should not have worry about about how many nodes are part of openshift
- routes is based on Kubernetes ingress, which provides an easy to access public url which is user-friendly as opposed to nodeport service
- hence, in openshift for internal service, we can create clusterip service
- for external access, we just need to expose the clusterip service as a route
- we don't have use node-port service in openshift
</pre>


## Info - Ingress vs Route


## Lab - Creating your own Custom Resource in Openshift
```
cd ~/openshift-tekton-june2024
git pull
cd Day6/crd

oc get trainings
oc get training
oc get train

oc apply -f training-crd.yml

oc get trainings
oc get training
oc get train

oc apply -f devops-training.yml
oc apply -f openshift-training.yml

oc get trainings
oc get training
oc get train
```

## Lab - Deploying wodpress & mariadb multi-pod application

Before deploy the wordpress and mariadb, you need to modify the mariadb-pv.yml, mariadb-pvc.yml, mariadb-deploy.yml, wordpress-pv.yml, wordpress-pvc.yml and wordpress-deploy.yml with your linux server IP and replace 'jegan' with your name.

```
cd ~/openshift-tektutor-june2024.git
git pull
cd Day6/wordpress
./deploy.sh
```

Expected output
![wordpress](wordpress1.png)
![wordpress](wordpress2.png)
![wordpress](wordpress3.png)
![wordpress](wordpress4.png)
![wordpress](wordpress5.png)
![wordpress](wordpress6.png)
![wordpress](wordpress7.png)
![wordpress](wordpress8.png)

## Ingress
Let's create a nginx deployment
```
oc project
oc create deployment nginx --image=bitnami/nginx:latest --replicas=3
oc get deploy,rs,po
```

Let's create clusterip internal service for nginx deployment
```
oc expose deploy/nginx --port=8080
oc get svc
oc describe svc/nginx
```

Let's create a hello microservice deployment
```
oc project
oc create deployment hello --image=tektutor/spring-ms:1.0 --replicas=3
oc get deploy,rs,po
```

Let's create clusterip internal service for hello deployment
```
oc expose deploy/hello --port=8080
oc get svc
oc describe svc/hello
```

Now let's create the ingress
```
cd ~/openshift-tekton-june2024
git pull
cd Day6/ingress
cat ingress.yml
oc apply -f ingress.yml
oc get ingress
```

Access the different services using ingress url, to access nginx service
```
curl http://tektutor.apps.ocp4.tektutor.org.labs/nginx
```

Access the different services using ingress url, to access hello service
```
curl http://tektutor.apps.ocp4.tektutor.org.labs/hello
```

Expected output
![ingress](ingress1.png)
![ingress](ingress2.png)
![ingress](ingress3.png)
![ingress](ingress4.png)

## Lab - S2I using Docker strategy by using declarartive build config manifest file

First we need create the imagestream to store the image in openshift internal container registry
```
cd ~/openshift-tekton-june2024
git pull
cd Day6/buildconfig
cat imagestream.yml
oc apply -f imagestream.yml
oc get imagestreams
oc get imagestream
oc get is
```

Now, let's create the builconfig and start the build
```
cd ~/openshift-tekton-june2024
git pull
cd Day6/buildconfig
oc apply -f buildconfig.yml
oc get buildconfigs
oc get buildconfig
oc get bc
```

To check the build log, you may try this
```
oc logs -f bc/hello
```

Expected output
![buildconfig](bc1.png)
![buildconfig](bc2.png)
![buildconfig](bc3.png)
![buildconfig](bc4.png)
![buildconfig](bc5.png)
![buildconfig](bc6.png)
![buildconfig](bc7.png)
![buildconfig](bc8.png)
![buildconfig](bc9.png)
![buildconfig](bc10.png)

## Info - What is Openshift Config Map?
<pre>
- it is map data strucutre
- we can store key-value pairs
- the data is organized based on the key
- we can use configmap to store several configuration data
- Examples
  - We could use configmap to store environment variables like
    JAVA_HOME=/usr/lib/jvm/jdk8
    M2_HOME=/usr/share/maven
- Develpers use xml, properties file to store configuration data, which could be stored within K8s as config map
- this is useful to store non-sensitive data as value stored against the key are visible in plain text 
</pre>

## Info - What is Openshift Secret?
<pre>
- internally secret uses the map data structure just like confimap  
- the key is stored as plain text, while the value is stored as base64 encoded values, hence somewhat secured
- this can be used to store sensitive data like password, login credentials, certs, etc.,
- the commercial alternate for this is HashiCorp Vault
</pre>

## Lab - Using ConfigMap and Secrets in wordpress & mariadb multi-pod application deployment
```
cd ~/openshift-tekton-june2024
git pull
cd Day6/wordress-with-configmap-and-secrets
./deploy.sh
```


## Lab - Create an edge route (https based public route url)

Find your base domain of your openshift cluster
```
oc get ingresses.config/cluster -o jsonpath={.spec.domain}
```

Expected output
<pre>
[root@tektutor.org auth]# oc get ingresses.config/cluster -o jsonpath={.spec.domain}
apps.ocp.tektutor.org.labs	
</pre>

Let's deploy a microservice and create an edge route as shown below.

First, let's generate a private key
```
openssl genrsa -out key.key
```

We need to create a public key using the private key with specific with your organization domain
```
openssl req -new -key key.key -out csr.csr -subj="/CN=hello-jegan.apps.ocp.tektutor.org.labs"
```

Sign the public key using the private key and generate certificate(.crt)
```
openssl x509 -req -in csr.csr -signkey key.key -out crt.crt
oc create route edge --service spring-ms --hostname hello-jegan.apps.ocp4.tektutor.org.labs --key key.key --cert crt.crt
```

Expected output
<pre>
[jegan@tektutor.org edge-route]$ oc get svc
NAME        TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)    AGE
spring-ms   ClusterIP   172.30.208.33   <none>        8080/TCP   87m
[jegan@tektutor.org edge-route]$ oc expose deploy/nginx --port=8080
service/nginx exposed
  
[jegan@tektutor.org edge-route]$ oc get svc
NAME        TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)    AGE
nginx       ClusterIP   172.30.16.165   <none>        8080/TCP   4s
spring-ms   ClusterIP   172.30.208.33   <none>        8080/TCP   87m

[jegan@tektutor.org edge-route]$ oc get ingresses.config/cluster -o jsonpath={.spec.domain}
apps.ocp4.tektutor.org.labs
  
[jegan@tektutor.org edge-route]$ oc project
Using project "jegan-devops" on server "https://api.ocp4.tektutor.org.labs:6443".
  
[jegan@tektutor.org edge-route]$ openssl req -new -key key.key -out csr.csr -subj="/CN=nginx-jegan-devops.apps.ocp4.tektutor.org.labs"
  
[jegan@tektutor.org edge-route]$ openssl x509 -req -in csr.csr -signkey key.key -out crt.crt
  
[jegan@tektutor.org edge-route]$ oc create route edge --service nginx --hostname nginx-jegan-devops.apps.ocp4.tektutor.org.labs --key key.key --cert crt.crt
route.route.openshift.io/nginx created
  
[jegan@tektutor.org edge-route]$ oc get route
NAME    HOST/PORT                                        PATH   SERVICES   PORT    TERMINATION   WILDCARD
nginx   nginx-jegan-devops.apps.ocp4.tektutor.org.labs   nginx      <all>   edge          None
</pre>

![edge](edge1.png)
![edge](edge2.png)
![edge](edge3.png)
![edge](edge4.png)
![edge](edge5.png)
![edge](edge6.png)
