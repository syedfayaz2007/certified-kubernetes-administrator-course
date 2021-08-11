# Namespaces
  - Take me to [Video Tutorial](https://kodekloud.com/courses/539883/lectures/9808159)
  
In this section, we will take a look at **`Namespaces`**

So far in this course we have created **`Objects`** such as **`PODs`**, **`Deployments`** and **`Services`** in our cluster. Whatever we have been doing we have been doing in a **`NAMESPACE`**.

- Kubernetes supports multiple virtual clusters backed by the same physical cluster. These virtual clusters are called namespaces.
- Namespaces provide a scope for names. Names of resources need to be unique within a namespace, but not across namespaces. Namespaces cannot be nested.
- Namespaces are a way to divide cluster resources between multiple users 

- This namespace is the **`default`** namespace in kuberntes. It is automatically created when kubernetes is setup initially.

  ![ns](../../images/ns.PNG)
  
- Kubernetes creates a set of pods and services for its internal purpose such as those requried by networking solutions, the DNS solutions etc. To isolate this from the user and to prevent you from accidently deleting and modifying the services, kubernetes creates them in another namespace(created at cluster startup) named **`kube-system`**.

  ![ns1](../../images/ns1.PNG)
  
- A third namespace created by kubernetes automatically is called **`kube-public`**. This is where resources that should be made available to user are created.
 
  ![ns2](../../images/ns2.PNG)

- You can create your own namespaces as well.

  ![ns3](../../images/ns3.PNG)

- Each of these namespaces can have its own set of **`policies`** that define who can do what.

  ![ns4](../../images/ns4.PNG)
  
- You can also assign quota of resources to each of these namespaces. That way each namespace is guaranteed a certain amount and does not use more than it's allowed limit.

  ![ns5](../../images/ns5.PNG)
  
- Going back to the default namespace that we have been working on, just like how members of a house refer to each other by their first names, the resources within a namespace can refer to each other simply by thier names. A resource in one namespace can also reach a resource of another namespace as well.
  
  ![ns6](../../images/ns6.PNG)
  
  ![ns7](../../images/ns7.PNG)
  
- To list the pods in default namespace
  ```
  $ kubectl get pods
  ```
- To list the pods in another namespace. Use **`kubectl get pods`** command along with the **`--namespace`** flag or argument.
  ```
  $ kubectl get pods --namespace=kube-system
  ```
  ![ns8](../../images/ns8.PNG)
  
- Here we have a pod defination file, when we create a pod with pod-defination file, the pod is created in the default namespace.
```
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
  labels:
     app: myapp
     type: front-end
spec:
  containers:
  - name: nginx-container
    image: nginx
 ```
  ```
  $ kubectl create -f pod-defination.yaml
  ```
- To create the pod with the pod-defination file in another namespace, use the **`--namespace`** option.
  ```
  $ kubectl create -f pod-defination.yaml --namespace=dev
  ```
  ![ns9](../../images/ns9.PNG)

- If you want to make sure that this pod gets you created in the **`dev`** env all the time, even if you don't specify in the command line, you can move the **`--namespace`** defination into the pod-defination file.
```
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
  namespace: dev
  labels:
     app: myapp
     type: front-end
spec:
  containers:
  - name: nginx-container
    image: nginx
 ```
  
  ![ns10](../../images/ns10.PNG)
  
- To create a new namespace, create a namespace defination as shown below and then run **`kubectl create`**
```
apiVersion: v1
kind: Namespace
metadata:
  name: dev
```

  ```
  $ kubectl create -f namespace-dev.yaml
  ```
  Another way to create a namespace
  ```
  $ kubectl create namespace dev
  ```
  ![ns11](../../images/ns11.PNG)
  
- By default, we will be in a **`default`** namespace. To switch to a particular namespace permenently run the below command.
  ```
  $ kubectl config set-context $(kubectl config current-context) --namespace=dev
  ```
- To view pods in all namespaces
  ```
  $ kubectl get pods --all-namespaces
  ```
  ![ns12](../../images/ns12.PNG)
  
- To limit resources in a namespace, create a resource quota. To create one start with **`ResourceQuota`** defination file.
```
apiVersion: v1
kind: ResourceQuota
metadata:
  name: compute-quota
  namespace: dev
spec:
  hard:
    pods: "10"
    requests.cpu: "4"
    requests.memory: 5Gi
    limits.cpu: "10"
    limits.memory: 10Gi
```
  ```
  $ kubectl create -f compute-quota.yaml
  ```
  ![ns13](../../images/ns13.PNG)
  
K8s Reference Docs:
- https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/
- https://kubernetes.io/docs/tasks/administer-cluster/namespaces-walkthrough/
- https://kubernetes.io/docs/tasks/administer-cluster/namespaces/
- https://kubernetes.io/docs/tasks/administer-cluster/manage-resources/quota-memory-cpu-namespace/
- https://kubernetes.io/docs/tasks/access-application-cluster/list-all-running-container-images/
  
  
  
  
  
  
