# Day 4

## Lab - Deploying an application from GitHub source using docker strategy
```
oc new-project jegan
oc new-app https://github.com/tektutor/spring-ms.git --strategy=docker
oc expose svc/spring-ms
```

To check build log
```
oc logs -f bc/spring-ms
```

## Lab - Deploying an application from GitHub source using source strategy
Before proceeding, you need delete the previous deployment to avoid errors
```
oc delete deploy/spring-ms svc/spring-ms route/spring-ms bc/spring-ms
```

Now you may proceed deploy application using source strategy
```
oc new-project jegan
oc new-app registry.access.redhat.com/ubi8/openjdk-11~https://github.com/tektutor/spring-ms.git --strategy=source
oc expose svc/spring-ms
```

To check build log
```
oc logs -f bc/spring-ms
```

## Lab - Deploying an application using Container image from Docker Hub Registry
```
oc new-app --name=nginx bitnami/nginx:latest
oc expose svc/nginx
```

You may check the status of the application in the webconsole developer topology.  In order to access the application, you can click on the route url arrow pointing diagonally upward.
