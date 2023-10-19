# kubernetes

## Setup
### 1) DockerHub account
Ex. my account: vitorgilsilva


### 2) Minikube
```
$ minikube version
$ minikube start --driver=docker
$ minikube status
$ minikube dashboard  //this launch a web page like Rancher

//stop the Minikube
$ minikube stop
```

### 3) kubectl
```
$ kubectl version
$ kubectl help
```
Create a folder in your home directory '.kube' and inside create a config file (this file will have the configurations for kubectl to connect to your cluster)


### TODO - both of approaches ?
```
// Create image and publish in dockerHub
$ docker build -t kub-first-app .
$ docker tag kub-first-app vitorgilsilva/kub-first-app
$ docker push vitorgilsilva/kub-first-app
```



## Imperative approach

- Kubernetes Command Line Tool: run commandds gains your cluster
    - Deploy
    - Inspect
    - Edit resources
    - Debug
    - View logs
    
- To check the status of the objects of your kubernetes cluster:
```
$ kubectl get deployments
$ kubectl get pods
$ kubectl get services
$ kubectl get ns
```

In the Imperative approach we need to run all the commands, "kubectl create deployment...".
Individual commands are executed to trigger certain kubernetes actions (comparable to using docker run only)

```
// create deployment named 'first-app' and the image must be accessible in the kubernetes cluster
$ kubectl create deployment first-app --image=....
$ kubectl create deployment first-app --image=vitorgilsilva/kub-first-app

// delete a deployment
$ kubectl delete deployment first-app
```

- To access externally we create a service (expose the port)
```
$ kubectl expose deployment first-app --type=LoadBalancer --port=8080
```
In the _--type_ we have different options:<br>
- [x] LoadBalancer    
- [ ] ClusterIP
- [ ] NodePort
- [ ] LoadBalancer

Or
```
//set an IP to the minikube to access the app - enable us to access the app externally !!!!
$ minikube service <name_of_deployment>
$ minikube service first-app
```

---
After that to teardown the service:
```
$ kubectl get services
$ kubectl delete service first-app //delete the services
```



**Update an Existing deployment pod/container**
> Create a new image version and publish in dockerHub:
```
$ docker build -t kub-first-app:2 .
$ docker tag kub-first-app:2 vitorgilsilva/kub-first-app:2
$ docker push vitorgilsilva/kub-first-app:2
```
> Update Deployments - an image in an existing deployment (current-container-name is in the dashboard):
```
$ kubectl set image deployment/first-app <current-container-name>=<new_image>
$ kubectl set image deployment/first-app kub-first-app=vitorgilsilva/kub-first-app
```
> check the status of the updated deployment:
```
$ kubectl rollout status deployment/first-app
```

> Deployment Rollbacks & History:
```   
$ kubectl rollout undo deployment/first-app	//rollback to the previous one

$ kubectl rollout history deployment/first-app //check the history of the deployments - give us the revision numbers
$ kubectl rollout history deployment/first-app --revision=1 //check the history of the deployments in detail

$ kubectl rollout undo deployment/first-app --to-revision=1   //specify the version of rollback
```


**To scale**

Scale some app "first-app" to 3 pods (a "replica" is simply an instance of a Pod/Container):
```
$ kubectl scale deployment/first-app --replicas=3
$ kubectl scale deployment/first-app --replicas=2
```

TODO
```
$ minikube start --nodes=2
```


---

## Declarative approach