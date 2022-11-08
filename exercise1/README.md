# exercise

create YAML files and deploy on your kubernetes cluster
- a namespace (not default) and everything below in that namespace
- a deployment with 2 replicas, image vvang/dummy:x86
- the deployment must have health checks and resource requests
- the container must have a environment variable TEXT=any-word-you-want
- a service at port 80 targeting the deployment pods (port 8080)
- an ingress with default backend to send traffic to the service
- access (curl) the service from a dummy pod running in default namespace
- access (EXTERNAL-IP) from outside

```
# make sure you access your Kubernetes cluster
export KUBECONFIG=~/.kube/config-curs20 # your number
kubectl get nodes
```

Create the yaml files. You may apply and check at every step as shown below.

I will use the name **foxy** for the namespace and all objects created, plase note they  are all in the same namespace.

```
# namespace
kubectl apply -f namespace.yaml
kubectl get ns

# deployment (-> replicaset -> pods)
kubectl apply -f deploy.yaml
kubectl -n foxy get pods
kubectl -n foxy get deploy
kubectl -n foxy get rs

# how do you check the pods have environment, health checks and resource requests?
kubectl -n foxy describe pod foxy-679cb78797-vkt4g

# service
kubectl apply -f svc.yaml 
kubectl -n foxy get svc foxy

## service ednpoints. is the service sending requests to the pods?
## check pod IPs and service Endpoints
kubectl -n foxy get pods -o wide
kubectl -n foxy describe svc foxy

# how do you access the service from inside Kubernetes
kubectl run dummy --image=vvang/dummy:x86
kubectl get pods # in namespace default
kubectl exec -ti dummy -- bash
  # inside the pod
  curl foxy.foxy # service foxy in namespace foxy
  exit

# ingress
kubectl apply -f ingress.yaml
kubectl -n foxy get ingress

# access from outside
# get the EXTERNAL-IP
kubectl -n ingress-nginx get svc
curl -H 'Host: foxy.example.com' 206.189.249.80

```

