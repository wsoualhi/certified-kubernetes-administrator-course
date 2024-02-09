# init
export ns=default
alias k='kubectl -n $ns' 


kubectl set image pod podname nginx=nginx:1.15-alpine

kubectl edit pod podName

# Create the nginx pod with version 1.17.4 and expose it on port 80
kubectl run nginx --image=nginx:1.17.4 --restart=Never --port=
kubectl run nginx-pod --image=nginx:alpine # will create a pod with name nginx-pod

# add the command in the pod
command: ['sleep', '5000']

# adding args
args: ['--color', 'green']

kubectl logs nginx # get logs

kubectl logs nginx -p # get previous logsj of the pod

kubectl exec -it nginx -- /bin/sh

kubectl exec -it nginx -- /bin/sh -c 'echo hello world'

kubectl create configmap special-config --from-literal=special.how=very --from-literal=special.type=charm

# set an env variable
kubectl run nginx --image=nginx --restart=Never --env=var1=val1

# get the env variable using exec
kubectl exec -it nginx -- env

# create a secret and add some values
kubectl create secret generic db-secret --from-literal=DB_Host=sql01

# create TLS secret 
 k -n webhook-demo create secret tls webhook-server-tls --cert "/root/keys/webhook-server-tls.crt"  --key "/root/keys/webhook-server-tls.key"

# multi container pod
kubectl run busybox --image=busybox --restart=Never --dry-run -o yaml -- bin/sh -c "sleep 3600; ls" > multi-container.yaml

# check logs for a container 1 and 2
kubectl logs busybox -c busybox1
kubectl logs busybox -c busybox2

# Check the previous logs of the second container busybox2 if any
kubectl logs busybox -c busybox2 --previous

# Run command ls in the third container busybox3 of the above pod
kubectl exec busybox -c busybox3 -- ls

# Show metrics of the above pod containers and puts them into the file.log and verify
kubectl top pod busybox --containers > file.log

kubectl exec -it  multi-cont-pod -c main-container -- sh cat /var/log/main.txt

# show labels
kubectl get pods --show-labels

# apply label
kubectl run nginx-dev1 --image=nginx --restart=Never --labels=env=dev

# Get the pods with label env=dev
kebectl get pods -l env=dev

# show labels which env in dev and prod
kubectl get pods -l 'env in (dev,prod)'

# update the label with overwrite
kubectl label po podone area=monteal --overwrite

# remove label named env
kubectl label pods podone env-

# show the labels for the nodes
kubectl get nodes --show-labels

# Annotate the pods with name=webapp
kubectl annnotate po podone name=webapp

# delete all the pods
kubectl delete po --all

# create a deployment with a name and replicas of 3
kubectl create deployment webapp --image=nginx --replicas=3

# scale deployment to have 20 replicas
kubectl scale deploy webapp --replicas=20

# get the rollout status
kubectl rollout status deploy webapp
k rollout history deployement/myapp-deployement
k rollout undo deployement/myapp-deployement

k expose deployment dep-name --name=service-name --port=x

# get the version numner
k explain pod --recursive | grep -i version

# force delete a pod
k delete pod podname --grace-period=0   --force

# scale RS
k scale rs new-replica-set --replicas=5

# selector
k get pods --selector app=App1
k get all --selector env=prod

# using set
k set image deployement/myapp-deployement nginx=nginx:1.9.1

# Job
k get jobs
k logs jobName

# Replace pod
k replace -f simple-web.yaml --force

# Check namespaced/non namespaced resources
k api-ressources --namespaced=true

# Check the kube-apiserver (as it is running as a pod)
ps -ef | grep kube-apiserver | grep admission-plugins

# Check new upgrades 
kubeadm upgrade plan

# upgrade order kubeadm, control plan, then kubelet

# view clusters
k config view

# etcd commands
  ```
  export ETCDCTL_API=3
   
  ETCDCTL_API=3 etcdctl --endpoints 10.2.0.9:2379 \
  --cert=/etc/kubernetes/pki/etcd/server.crt \
  --key=/etc/kubernetes/pki/etcd/server.key \
  --cacert=/etc/kubernetes/pki/etcd/ca.crt \
  member list

  kubectl exec etcd-master -n kube-system -- sh -c "ETCDCTL_API=3 etcdctl get / --prefix --keys-only --limit=10 --cacert /etc/kubernetes/pki/etcd/ca.crt --cert /etc/kubernetes/pki/etcd/server.crt  --key /etc/kubernetes/pki/etcd/server.key" 

  etcdctl snapshot save 
  etcdctl endpoint health
  etcdctl get
  etcdctl put
   ```

# scp, remote to loca, on the local server
   ```
   scp remotenode:/opt/cluster1.db /opt
   ```
# install kube 

look for "install kubeadm" https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/

# find the init system - here it's systemd
> ps -p 1
1 00:00:02 systemd

# important file that contains information on service ips
cat /etc/kubernetes/manifests/kube-apiserver.yaml | grep cluster-ip-range

# identify the kube-api ps and find the logs
``` sh
crictl ps -a
crictl logs container-id
```
# base64 maniputation
```
# encoding a certificate in base64
cat certificate-csr.csr | base64 -w 0
```
# grep before and after
```
grep -B 3 -A 2 foo 
```
# count the lines
```
k get roles -A | wc -l
```
# create role and rolebindings

To create a Role:
```
kubectl create role developer --namespace=default --verb=list,create,delete --resource=pods
```

To create a RoleBinding:
```
kubectl create rolebinding dev-user-binding --namespace=default --role=developer --user=dev-user
```
# set service accounts
```
kubectl set serviceaccount deploy/web-dashboard dashboard-sa
```
# kubectx and kubens
Installation
```sh
sudo git clone https://github.com/ahmetb/kubectx /opt/kubectx
sudo ln -s /opt/kubectx/kubectx /usr/local/bin/kubectx
#To list all contexts
kubectx
#To switch to a new context:
kubectx <context_name>
#To switch back to previous context:
kubectx -
#To see current context:
kubectx -c
```
Installation
```sh
sudo git clone https://github.com/ahmetb/kubectx /opt/kubens
sudo ln -s /opt/kubectx/kubens /usr/local/bin/kubens
#To switch to a new namespace:
kubens <new_namespace>
#To switch back to previous namespace:
kubens -
```
# Troubleshooting Control plan
- To check the status of **`kube-apiserver`** 
    ```
    service kube-apiserver status
    ```
- To check the status of **`kube-controller-manager`** 
    ```
    service kube-controller-manager status
    ```
- To check the status of **`kube-scheduler`** 
    ```
    service kube-scheduler status
    ```
- To check the status of **`kubelet`** 
    ```
    service kubelet status
    ```
- To check the status of **`kube-proxy`** on the worker nodes.
    ```
    service kube-proxy status
    ```
- To check the logs of the Control Plane components deployed as Pods:
    ```
    kubectl logs kube-apiserver-master -n kube-system
    ```
- To check the logs of the Control Plane components deployed as SystemD Service
    ```
    sudo journalctl -u kube-apiserver
    ```
- in case of issues, change things in the manifest

    ```
    cd /etc/kubernetes/manifest
    vi ...
    ```
# Troubleshooting nodes
- SSH into the node
    ```
    systemctl status containerd
    systemctl status kubelet
    systemctl start kubelet
    sudo journalctl -u kubelet -f
    /var/lib/kubelet/config.yaml
    ps -aux | grep kubelet
    ```
- kubelet config is in 
    ```
   /var/lib/kubelet/config.yaml
    ```
# Worker Node Failure

  - Check node
    ```
    kubectl get nodes
    kubectl describe node worker-1
    ```
  - Check the possible **`CPU`** and **`MEMORY`**  using **`top`** and **`df -h`** 
    ```
    top
    df -h
    ```
  - Check the status and the logs of the **`kubelet`** for the possible issues.
    ```
    serivce kubelet status
    sudo journalctl -u kubelet
    ```
  - Check the **`kubelet`** Certificates, they are not expired, and in the right group and issued by the right CA.

    ```
    openssl x509 -in /var/lib/kubelet/worker-1.crt -text
    ```
# Json
```
kubectl get pv --sort-by=.spec.capacity.storage -o=custom-columns=NAME:.metadata.name,CAPACITY:.spec.capacity.storageNAME       CAPACITY
pv-log-4   40Mi
pv-log-1   100Mi
pv-log-2   200Mi
pv-log-3   300Mi

kubectl config view --kubeconfig=my-kube-config -o jsonpath="{.contexts[?(@.context.user=='aws-user')].name}"
```
# Create an NGINX Pod
```
kubectl run nginx --image=nginx
```
# Generate POD Manifest YAML file (-o yaml). Don't create it(--dry-run)
```
kubectl run nginx --image=nginx --dry-run=client -o yaml
```
# Create a deployment
```
kubectl create deployment --image=nginx nginx
```
# Generate Deployment YAML file (-o yaml). Don't create it(--dry-run)
```
kubectl create deployment --image=nginx nginx --dry-run=client -o yaml
```
# Generate Deployment YAML file (-o yaml). Don’t create it(–dry-run) and save it to a file.
```
kubectl create deployment --image=nginx nginx --dry-run=client -o yaml > nginx-deployment.yaml

kubectl create deployment --image=nginx nginx --replicas=4 --dry-run=client -o yaml > nginx-deployment.yaml
```
# Create an NGINX Pod
```
kubectl run nginx --image=nginx
kubectl run nginx --image=nginx --dry-run=client -o yaml
```
# Create a Services
```
kubectl expose pod redis --port=6379 --name redis-service --dry-run=client -o yaml
kubectl create service clusterip redis --tcp=6379:6379 --dry-run=client -o yaml 
kubectl expose pod nginx --type=NodePort --port=80 --name=nginx-service --dry-run=client -o yaml
kubectl create service nodeport nginx --tcp=80:80 --node-port=30080 --dry-run=client -o yaml
```
