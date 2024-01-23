❯ git clone https://github.com/kodekloudhub/certified-kubernetes-administrator-course.git
Cloning into 'certified-kubernetes-administrator-course'...
remote: Enumerating objects: 4751, done.
remote: Counting objects: 100% (913/913), done.
remote: Compressing objects: 100% (178/178), done.
remote: Total 4751 (delta 802), reused 772 (delta 733), pack-reused 3838
Receiving objects: 100% (4751/4751), 66.35 MiB | 21.15 MiB/s, done.
Resolving deltas: 100% (2567/2567), done.
❯ ls
CKA-cheatsheet.bash                       Updates+2021.pdf
KodeKloud-Kubernetes+-CKAD.pdf            certified-kubernetes-administrator-course
Kubernetes-CKA-taints-tolerations.pdf     pod-deployment.yaml
Networking.pdf                            rc-definition.yml
Services.pdf
❯ cd certified-kubernetes-administrator-course
❯ ls
README.md     Vagrantfile   apple-silicon docs          images        resources     ubuntu
❯ vagrant status
Current machine states:

kubemaster                not created (virtualbox)
kubenode01                not created (virtualbox)
kubenode02                not created (virtualbox)

This environment represents multiple VMs. The VMs are all listed
above with their current state. For more information about a specific
VM, run `vagrant status NAME`.
❯ vagrant up
Bringing machine 'kubemaster' up with 'virtualbox' provider...
Bringing machine 'kubenode01' up with 'virtualbox' provider...
Bringing machine 'kubenode02' up with 'virtualbox' provider...
==> kubemaster: Box 'ubuntu/bionic64' could not be found. Attempting to find and install...
    kubemaster: Box Provider: virtualbox
    kubemaster: Box Version: >= 0
==> kubemaster: Loading metadata for box 'ubuntu/bionic64'
    kubemaster: URL: https://vagrantcloud.com/ubuntu/bionic64
==> kubemaster: Adding box 'ubuntu/bionic64' (v20230607.0.0) for provider: virtualbox
    kubemaster: Downloading: https://vagrantcloud.com/ubuntu/boxes/bionic64/versions/20230607.0.0/providers/virtualbox.box
Download redirected to host: cloud-images.ubuntu.com
==> kubemaster: Successfully added box 'ubuntu/bionic64' (v20230607.0.0) for 'virtualbox'!
==> kubemaster: Importing base box 'ubuntu/bionic64'...
==> kubemaster: Matching MAC address for NAT networking...
==> kubemaster: Setting the name of the VM: kubemaster
Vagrant is currently configured to create VirtualBox synced folders with
the `SharedFoldersEnableSymlinksCreate` option enabled. If the Vagrant
guest is not trusted, you may want to disable this option. For more
information on this option, please refer to the VirtualBox manual:

  https://www.virtualbox.org/manual/ch04.html#sharedfolders

This option can be disabled globally with an environment variable:

  VAGRANT_DISABLE_VBOXSYMLINKCREATE=1

or on a per folder basis within the Vagrantfile:

  config.vm.synced_folder '/host/path', '/guest/path', SharedFoldersEnableSymlinksCreate: false
==> kubemaster: Clearing any previously set network interfaces...
==> kubemaster: Preparing network interfaces based on configuration...
    kubemaster: Adapter 1: nat
    kubemaster: Adapter 2: hostonly
==> kubemaster: Forwarding ports...
    kubemaster: 22 (guest) => 2711 (host) (adapter 1)
    kubemaster: 22 (guest) => 2222 (host) (adapter 1)
==> kubemaster: Running 'pre-boot' VM customizations...
==> kubemaster: Booting VM...
==> kubemaster: Waiting for machine to boot. This may take a few minutes...
    kubemaster: SSH address: 127.0.0.1:2222
    kubemaster: SSH username: vagrant
    kubemaster: SSH auth method: private key
    kubemaster: Warning: Connection reset. Retrying...
    kubemaster: Warning: Remote connection disconnect. Retrying...
    kubemaster:
    kubemaster: Vagrant insecure key detected. Vagrant will automatically replace
    kubemaster: this with a newly generated keypair for better security.
    kubemaster:
    kubemaster: Inserting generated public key within guest...
    kubemaster: Removing insecure key from the guest if it's present...
    kubemaster: Key inserted! Disconnecting and reconnecting using new SSH key...
==> kubemaster: Machine booted and ready!
==> kubemaster: Checking for guest additions in VM...
    kubemaster: The guest additions on this VM do not match the installed version of
    kubemaster: VirtualBox! In most cases this is fine, but in rare cases it can
    kubemaster: prevent things such as shared folders from working properly. If you see
    kubemaster: shared folder errors, please make sure the guest additions within the
    kubemaster: virtual machine match the version of VirtualBox you have installed on
    kubemaster: your host and reload your VM.
    kubemaster:
    kubemaster: Guest Additions Version: 5.2.42
    kubemaster: VirtualBox Version: 7.0
==> kubemaster: Setting hostname...
==> kubemaster: Configuring and enabling network interfaces...
==> kubemaster: Mounting shared folders...
    kubemaster: /vagrant => /Users/wassimsoualhi/work/Trainings/udemy_CKA/certified-kubernetes-administrator-course
==> kubemaster: Running provisioner: setup-hosts (shell)...
    kubemaster: Running: /var/folders/3k/6cjd0b75167gn119z_t51zq40000gn/T/vagrant-shell20230703-54230-afw1uk.sh
    kubemaster: + IFNAME=enp0s8
    kubemaster: + THISHOST=
    kubemaster: ++ ip -4 addr show enp0s8
    kubemaster: ++ awk '{print $2}'
    kubemaster: ++ head -1
    kubemaster: ++ grep inet
    kubemaster: ++ cut -d/ -f1
    kubemaster: + ADDRESS=192.168.56.2
    kubemaster: ++ echo 192.168.56.2
    kubemaster: ++ awk 'BEGIN {FS="."} ; { printf("%s.%s.%s", $1, $2, $3) }'
    kubemaster: + NETWORK=192.168.56
    kubemaster: + sed -e 's/^.*kubemaster.*/192.168.56.2 kubemaster kubemaster.local/' -i /etc/hosts
    kubemaster: + sed -e '/^.*ubuntu-jammy.*/d' -i /etc/hosts
    kubemaster: + sed -e '/^.*.*/d' -i /etc/hosts
    kubemaster: + cat
==> kubemaster: Running provisioner: setup-dns (shell)...
    kubemaster: Running: /var/folders/3k/6cjd0b75167gn119z_t51zq40000gn/T/vagrant-shell20230703-54230-l8pxme.sh
==> kubenode01: Box 'ubuntu/bionic64' could not be found. Attempting to find and install...
    kubenode01: Box Provider: virtualbox
    kubenode01: Box Version: >= 0
==> kubenode01: Loading metadata for box 'ubuntu/bionic64'
    kubenode01: URL: https://vagrantcloud.com/ubuntu/bionic64
==> kubenode01: Adding box 'ubuntu/bionic64' (v20230607.0.0) for provider: virtualbox
==> kubenode01: Importing base box 'ubuntu/bionic64'...
==> kubenode01: Matching MAC address for NAT networking...
==> kubenode01: Setting the name of the VM: kubenode01
==> kubenode01: Fixed port collision for 22 => 2222. Now on port 2200.
==> kubenode01: Clearing any previously set network interfaces...
==> kubenode01: Preparing network interfaces based on configuration...
    kubenode01: Adapter 1: nat
    kubenode01: Adapter 2: hostonly
==> kubenode01: Forwarding ports...
    kubenode01: 22 (guest) => 2721 (host) (adapter 1)
    kubenode01: 22 (guest) => 2200 (host) (adapter 1)
==> kubenode01: Running 'pre-boot' VM customizations...
==> kubenode01: Booting VM...
==> kubenode01: Waiting for machine to boot. This may take a few minutes...
    kubenode01: SSH address: 127.0.0.1:2200
    kubenode01: SSH username: vagrant
    kubenode01: SSH auth method: private key
    kubenode01: Warning: Connection reset. Retrying...
    kubenode01:
    kubenode01: Vagrant insecure key detected. Vagrant will automatically replace
    kubenode01: this with a newly generated keypair for better security.
    kubenode01:
    kubenode01: Inserting generated public key within guest...
    kubenode01: Removing insecure key from the guest if it's present...
    kubenode01: Key inserted! Disconnecting and reconnecting using new SSH key...
==> kubenode01: Machine booted and ready!
==> kubenode01: Checking for guest additions in VM...
    kubenode01: The guest additions on this VM do not match the installed version of
    kubenode01: VirtualBox! In most cases this is fine, but in rare cases it can
    kubenode01: prevent things such as shared folders from working properly. If you see
    kubenode01: shared folder errors, please make sure the guest additions within the
    kubenode01: virtual machine match the version of VirtualBox you have installed on
    kubenode01: your host and reload your VM.
    kubenode01:
    kubenode01: Guest Additions Version: 5.2.42
    kubenode01: VirtualBox Version: 7.0
==> kubenode01: Setting hostname...
==> kubenode01: Configuring and enabling network interfaces...
==> kubenode01: Mounting shared folders...
    kubenode01: /vagrant => /Users/wassimsoualhi/work/Trainings/udemy_CKA/certified-kubernetes-administrator-course
==> kubenode01: Running provisioner: setup-hosts (shell)...
    kubenode01: Running: /var/folders/3k/6cjd0b75167gn119z_t51zq40000gn/T/vagrant-shell20230703-54230-rt5vbc.sh
    kubenode01: + IFNAME=enp0s8
    kubenode01: + THISHOST=
    kubenode01: ++ ip -4 addr show enp0s8
    kubenode01: ++ head -1
    kubenode01: ++ awk '{print $2}'
    kubenode01: ++ grep inet
    kubenode01: ++ cut -d/ -f1
    kubenode01: + ADDRESS=192.168.56.3
    kubenode01: ++ echo 192.168.56.3
    kubenode01: ++ awk 'BEGIN {FS="."} ; { printf("%s.%s.%s", $1, $2, $3) }'
    kubenode01: + NETWORK=192.168.56
    kubenode01: + sed -e 's/^.*kubenode01.*/192.168.56.3 kubenode01 kubenode01.local/' -i /etc/hosts
    kubenode01: + sed -e '/^.*ubuntu-jammy.*/d' -i /etc/hosts
    kubenode01: + sed -e '/^.*.*/d' -i /etc/hosts
    kubenode01: + cat
==> kubenode01: Running provisioner: setup-dns (shell)...
    kubenode01: Running: /var/folders/3k/6cjd0b75167gn119z_t51zq40000gn/T/vagrant-shell20230703-54230-gkd84q.sh
==> kubenode02: Box 'ubuntu/bionic64' could not be found. Attempting to find and install...
    kubenode02: Box Provider: virtualbox
    kubenode02: Box Version: >= 0
==> kubenode02: Loading metadata for box 'ubuntu/bionic64'
    kubenode02: URL: https://vagrantcloud.com/ubuntu/bionic64
==> kubenode02: Adding box 'ubuntu/bionic64' (v20230607.0.0) for provider: virtualbox
==> kubenode02: Importing base box 'ubuntu/bionic64'...
==> kubenode02: Matching MAC address for NAT networking...
==> kubenode02: Setting the name of the VM: kubenode02
==> kubenode02: Fixed port collision for 22 => 2222. Now on port 2201.
==> kubenode02: Clearing any previously set network interfaces...
==> kubenode02: Preparing network interfaces based on configuration...
    kubenode02: Adapter 1: nat
    kubenode02: Adapter 2: hostonly
==> kubenode02: Forwarding ports...
    kubenode02: 22 (guest) => 2722 (host) (adapter 1)
    kubenode02: 22 (guest) => 2201 (host) (adapter 1)
==> kubenode02: Running 'pre-boot' VM customizations...
==> kubenode02: Booting VM...
==> kubenode02: Waiting for machine to boot. This may take a few minutes...
    kubenode02: SSH address: 127.0.0.1:2201
    kubenode02: SSH username: vagrant
    kubenode02: SSH auth method: private key
    kubenode02: Warning: Connection reset. Retrying...
    kubenode02: Warning: Remote connection disconnect. Retrying...
    kubenode02:
    kubenode02: Vagrant insecure key detected. Vagrant will automatically replace
    kubenode02: this with a newly generated keypair for better security.
    kubenode02:
    kubenode02: Inserting generated public key within guest...
    kubenode02: Removing insecure key from the guest if it's present...
    kubenode02: Key inserted! Disconnecting and reconnecting using new SSH key...
==> kubenode02: Machine booted and ready!
==> kubenode02: Checking for guest additions in VM...
    kubenode02: The guest additions on this VM do not match the installed version of
    kubenode02: VirtualBox! In most cases this is fine, but in rare cases it can
    kubenode02: prevent things such as shared folders from working properly. If you see
    kubenode02: shared folder errors, please make sure the guest additions within the
    kubenode02: virtual machine match the version of VirtualBox you have installed on
    kubenode02: your host and reload your VM.
    kubenode02:
    kubenode02: Guest Additions Version: 5.2.42
    kubenode02: VirtualBox Version: 7.0
==> kubenode02: Setting hostname...
==> kubenode02: Configuring and enabling network interfaces...
==> kubenode02: Mounting shared folders...
    kubenode02: /vagrant => /Users/wassimsoualhi/work/Trainings/udemy_CKA/certified-kubernetes-administrator-course
==> kubenode02: Running provisioner: setup-hosts (shell)...
    kubenode02: Running: /var/folders/3k/6cjd0b75167gn119z_t51zq40000gn/T/vagrant-shell20230703-54230-25vt8j.sh
    kubenode02: + IFNAME=enp0s8
    kubenode02: + THISHOST=
    kubenode02: ++ ip -4 addr show enp0s8
    kubenode02: ++ head -1
    kubenode02: ++ awk '{print $2}'
    kubenode02: ++ grep inet
    kubenode02: ++ cut -d/ -f1
    kubenode02: + ADDRESS=192.168.56.4
    kubenode02: ++ echo 192.168.56.4
    kubenode02: ++ awk 'BEGIN {FS="."} ; { printf("%s.%s.%s", $1, $2, $3) }'
    kubenode02: + NETWORK=192.168.56
    kubenode02: + sed -e 's/^.*kubenode02.*/192.168.56.4 kubenode02 kubenode02.local/' -i /etc/hosts
    kubenode02: + sed -e '/^.*ubuntu-jammy.*/d' -i /etc/hosts
    kubenode02: + sed -e '/^.*.*/d' -i /etc/hosts
    kubenode02: + cat
==> kubenode02: Running provisioner: setup-dns (shell)...
    kubenode02: Running: /var/folders/3k/6cjd0b75167gn119z_t51zq40000gn/T/vagrant-shell20230703-54230-r4kx9y.sh
❯ vagrant ssh kubenode01
Welcome to Ubuntu 18.04.6 LTS (GNU/Linux 4.15.0-212-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Mon Jul  3 13:12:05 UTC 2023

  System load:  0.14              Processes:             101
  Usage of /:   3.0% of 38.70GB   Users logged in:       0
  Memory usage: 6%                IP address for enp0s3: 10.0.2.15
  Swap usage:   0%                IP address for enp0s8: 192.168.56.3


Expanded Security Maintenance for Infrastructure is not enabled.

0 updates can be applied immediately.

Enable ESM Infra to receive additional future security updates.
See https://ubuntu.com/esm or run: sudo pro status

New release '20.04.6 LTS' available.
Run 'do-release-upgrade' to upgrade to it.


vagrant@kubenode01:~$
vagrant@kubenode01:~$
vagrant@kubenode01:~$ ifconfig
enp0s3: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 10.0.2.15  netmask 255.255.255.0  broadcast 10.0.2.255
        inet6 fe80::3b:7bff:feb7:3b2d  prefixlen 64  scopeid 0x20<link>
        ether 02:3b:7b:b7:3b:2d  txqueuelen 1000  (Ethernet)
        RX packets 1586  bytes 449719 (449.7 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 1040  bytes 182623 (182.6 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

enp0s8: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.56.3  netmask 255.255.255.0  broadcast 192.168.56.255
        inet6 fe80::a00:27ff:fe17:19d7  prefixlen 64  scopeid 0x20<link>
        ether 08:00:27:17:19:d7  txqueuelen 1000  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 11  bytes 866 (866.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 16  bytes 1532 (1.5 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 16  bytes 1532 (1.5 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0