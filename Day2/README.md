# Day 2

## Lab - Finding more details about a node
```
oc get nodes
oc describe node/master-1.ocp4.tektutor.org.labs
```

Expected output
![node](node1.png)

## Lab - Editing a node (don't modify anything)
```
oc get nodes
oc edit node/worker-1.ocp4.tektutor.org.labs
```
Expected output
![node](node2.png)
![node](node3.png)

## Lab - Using wide mode to find node IP and OS installed
```
oc get nodes -o wide
```

Expected output
![node](node4.png)
