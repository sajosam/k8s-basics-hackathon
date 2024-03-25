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
NAME                   STATUS   ROLES    AGE     VERSION
pool-ou9swnhyx-jnuar   Ready    <none>   2d1h    v1.29.0
pool-ou9swnhyx-jnut3   Ready    <none>   2d1h    v1.29.0
pool-ou9swnhyx-o9vie   Ready    <none>   2d12h   v1.29.0
pool-ou9swnhyx-owrla   Ready    <none>   38d     v1.29.0
pool-ou9swnhyx-owrpj   Ready    <none>   38d     v1.29.0
pool-ou9swnhyx-ox0rx   Ready    <none>   47d     v1.29.0

```

## Task 2
describe one kubernetes node using `kubectl describe node/<node-name>` command and paste the section from the terminal output below

**Number of cpu**:     
```
Capacity:
  cpu:                2
  ephemeral-storage:  82394940Ki
  hugepages-2Mi:      0
  memory:             4009188Ki
  pods:               110
```
**Hostname**: 
```
Addresses:
  InternalIP:  10.116.0.8
  Hostname:    pool-ou9swnhyx-jnuar
  ExternalIP:  165.227.92.87
```
**Cpu and Memory usage**:
```
  Resource           Requests     Limits
  --------           --------     ------
  cpu                1253m (65%)  1250m (65%)
  memory             735Mi (23%)  600Mi (19%)
  ephemeral-storage  0 (0%)       0 (0%)
  hugepages-2Mi      0 (0%)       0 (0%)
```

## Task 3
List all kubernetes namespaces using `kubectl get namespace` command and paste the output below
	    
```
NAME              STATUS        AGE
appdy             Active        2d12h
appdynamics       Active        2d13h
default           Active        47d
ingress-nginx     Terminating   23d
kube-node-lease   Active        43d
kube-public       Active        47d
kube-system       Active        47d
mimir-test        Active        28d
nginx-mesh        Terminating   24d
op-org-14         Active        11d

```

## Task 4
List all the pods in '*kube-system*' namespace using `kubectl get pods -n <namespce command>`
	    
```
NAME                               READY   STATUS    RESTARTS        AGE
cilium-2s4h4                       1/1     Running   0               38d
cilium-67dxn                       1/1     Running   0               2d12h
cilium-f6d8r                       1/1     Running   0               47d
cilium-nmcrh                       1/1     Running   0               2d1h
cilium-operator-6d6589c67c-nktmp   1/1     Running   6 (3d10h ago)   38d
cilium-smnln                       1/1     Running   0               2d1h
cilium-wwbqz                       1/1     Running   0               38d

```


## Task 5

Create a namespace with name `my-namespace` using `kubectl create <namespace name>` command

List all namespaces like  in **Task 3**  and paste output below
```
NAME              STATUS        AGE
appdy             Active        2d12h
appdynamics       Active        2d13h
default           Active        47d
hackathon         Active        62s
ingress-nginx     Terminating   23d
kube-node-lease   Active        43d
kube-public       Active        47d
kube-system       Active        47d
mimir-test        Active        28d
my-namespace      Active        4s

```
## Task 6

Create a Pod with name `nginx` image `nginx:latest` in `my-namespace` using yaml configurations.

1. Create yaml configuration to create a pod should run on the namespace you created in the last **Task 5**

	Refference: https://kubernetes.io/docs/concepts/workloads/pods/#using-pods
3. Use `kubectl apply -f <filename>` command to apply the configuration


Copy the yaml content below
```
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  namespace: my-namespace
spec:
  containers:
  - name: nginx
    image: nginx:latest
    ports:
    - containerPort: 80


```

List all the pods in the namespace `my-namespace` using `kubectl get pods -n <namespace>` command
```
NAME    READY   STATUS    RESTARTS   AGE
nginx   1/1     Running   0          26s

```

Get extra details about the pods in the namespace `my-namespace` using `kubectl get pods -n <namespace> -o wide` command
```
NAME    READY   STATUS    RESTARTS   AGE   IP             NODE                   NOMINATED NODE   READINESS GATES
nginx   1/1     Running   0          47s   10.244.2.119   pool-ou9swnhyx-jnuar   <none>           <none>

```

## Task 7

Get details about `nginx` pod in `my-namespace`  using `kubectl describe pods/<pod-name> -n <namespace>` command


```
Name:             nginx
Namespace:        my-namespace
Priority:         0
Service Account:  default
Node:             pool-ou9swnhyx-jnuar/10.116.0.8
Start Time:       Mon, 25 Mar 2024 12:55:55 +0530
Labels:           <none>
Annotations:      <none>
Status:           Running
IP:               10.244.2.119
IPs:
  IP:  10.244.2.119
Containers:
  nginx:
    Container ID:   containerd://0fc5cee609db8f13587d67d35054991c646c6d834e09ed0a68cabc6581ad0f65
    Image:          nginx:latest
    Image ID:       docker.io/library/nginx@sha256:6db391d1c0cfb30588ba0bf72ea999404f2764febf0f1f196acd5867ac7efa7e
    Port:           80/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Mon, 25 Mar 2024 12:56:02 +0530
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-5fp9p (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   True
  Initialized                 True
  Ready                       True
  ContainersReady             True
  PodScheduled                True
Volumes:
  kube-api-access-5fp9p:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type    Reason     Age   From               Message
  ----    ------     ----  ----               -------
  Normal  Scheduled  108s  default-scheduler  Successfully assigned my-namespace/nginx to pool-ou9swnhyx-jnuar
  Normal  Pulling    107s  kubelet            Pulling image "nginx:latest"
  Normal  Pulled     102s  kubelet            Successfully pulled image "nginx:latest" in 5.43s (5.43s including waiting)
  Normal  Created    102s  kubelet            Created container nginx
  Normal  Started    101s  kubelet            Started container nginx

```

## Task 8

Port forward the `nginx` (running in namespace `my-namespace`) pods's port `80` to your local systems port `9090` using `kubectl port-forward` command 

Refference: 
https://kubernetes.io/docs/reference/kubectl/generated/kubectl_port-forward/

```
Forwarding from 127.0.0.1:80 -> 9090
Forwarding from [::1]:80 -> 9090

```

Open another terminal  and do a curl to the port using given command
`curl http://localhost:9000`

```
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>

```


## Task 9

List all the logs of pod `nginx` running in `my-namespace`  using `kubectl logs` command

Refference: 
https://kubernetes.io/docs/reference/kubectl/generated/kubectl_logs
```
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2024/03/25 07:26:02 [notice] 1#1: using the "epoll" event method
2024/03/25 07:26:02 [notice] 1#1: nginx/1.25.4
2024/03/25 07:26:02 [notice] 1#1: built by gcc 12.2.0 (Debian 12.2.0-14)
2024/03/25 07:26:02 [notice] 1#1: OS: Linux 6.1.0-17-amd64
2024/03/25 07:26:02 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
2024/03/25 07:26:02 [notice] 1#1: start worker processes
2024/03/25 07:26:02 [notice] 1#1: start worker process 30
2024/03/25 07:26:02 [notice] 1#1: start worker process 31
127.0.0.1 - - [25/Mar/2024:07:36:01 +0000] "GET / HTTP/1.1" 200 615 "-" "curl/8.2.1" "-"

```

## Task 10
Delete the pod `nginx` using the yaml configurations we created in the **Task 6**

`kubectl delete -f < yaml file name with path from task 6>`

Refference:
https://kubernetes.io/docs/reference/kubectl/generated/kubectl_delete

```
pod "nginx" deleted

```

Delete the namespace `my-namespace` using `kubectl delete namespace <namespace>` command

```
namespace "my-namespace" deleted

```
