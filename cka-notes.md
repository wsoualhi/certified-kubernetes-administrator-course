# vm deployement in openstack
openstack server create --image ubuntu-20.04 --flavor ws-4c-4r-80d --network mke_cilium-int-net --security-group ws-secure-fe --key-name xxx ws-k0s-cka
openstack floating ip create public 
openstack server add floating ip ws-k0s-cka x.x.x.x

# access to vm with k0s
