# Kubernetes hackathon

## Prerequisites
- Kubectl installation
	- https://kubernetes.io/docs/tasks/tools/
- Minikube installation
	- https://minikube.sigs.k8s.io/docs/start/
- Start the cluster using 
	 ```minikube start```
- Ensure minikube cluster context is set in **kubectl** command


## Task 1
List all kubernetes nodes using `kubectl get nodes` command and paste the output below
	    
```
<Paste output below>

```

## Task 2
describe one kubernetes node using `kubectl describe node/<node-name>` command and paste the section from the terminal output below

**Number of cpu**:     
```
<Paste section here>
```
**Hostname**: 
```
<Paste section here>
```
**Cpu and Memory usage**:
```
<Paste section here>
```

## Task 3
List all kubernetes namespaces using `kubectl get namespace` command and paste the output below
	    
```
<Paste output below>

```

## Task 4
List all the pods in '*kube-system*' namespace using `kubectl get pods -n <namespce command>`
	    
```
<Paste output below>

```


## Task 5

Create a namespace with name `my-namespace` using `kubectl create namespace <namespace name>` command

List all namespaces like  in **Task 3**  and paste output below
```
<Paste output below>

```
## Task 6

Create a Pod with name `nginx` image `nginx:latest` in `my-namespace` using yaml configurations.

1. Create yaml configuration to create a pod should run on the namespace you created in the last **Task 5**

	Refference: https://kubernetes.io/docs/concepts/workloads/pods/#using-pods
3. Use `kubectl apply -f <filename>` command to apply the configuration


Copy the yaml content below
```
<Paste output here>

```

List all the pods in the namespace `my-namespace` using `kubectl get pods -n <namespace>` command
```
<Paste output here>

```

Get extra details about the pods in the namespace `my-namespace` using `kubectl get pods -n <namespace> -o wide` command
```
<Paste output here>

```

## Task 7

Get details about `nginx` pod in `my-namespace`  using `kubectl describe pods/<pod-name> -n <namespace>` command


```
<Paste the output of describe command below>

```

## Task 8

Port forward the `nginx` (running in namespace `my-namespace`) pods's port `80` to your local systems port `9090` using `kubectl port-forward` command 

Refference: 
https://kubernetes.io/docs/reference/kubectl/generated/kubectl_port-forward/

```
<Paste the output of port-forward command below>

```

Open another terminal  and do a curl to the port using given command
`curl http://localhost:9090`

```
<Paste the output of curl command below>

```


## Task 9

List all the logs of pod `nginx` running in `my-namespace`  using `kubectl logs` command

Refference: 
https://kubernetes.io/docs/reference/kubectl/generated/kubectl_logs
```
<Paste the output of kubectl logs command>

```

## Task 10
Delete the pod `nginx` using the yaml configurations we created in the **Task 6**

`kubectl delete -f < yaml file name with path from task 6>`

Refference:
https://kubernetes.io/docs/reference/kubectl/generated/kubectl_delete

```
<Paste the output of kubectl delete command>

```

Delete the namespace `my-namespace` using `kubectl delete namespace <namespace>` command

```
<Paste the output of kubectl delete command>

```
