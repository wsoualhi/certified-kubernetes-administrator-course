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
ETCDCTL_API=3 etcdctl --endpoints 10.2.0.9:2379 \
  --cert=/etc/kubernetes/pki/etcd/server.crt \
  --key=/etc/kubernetes/pki/etcd/server.key \
  --cacert=/etc/kubernetes/pki/etcd/ca.crt \
  member list

#scp, remote to loca, on the local server
scp remotenode:/opt/cluster1.db /opt

# install kube : look for "install kubeadm" https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/

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