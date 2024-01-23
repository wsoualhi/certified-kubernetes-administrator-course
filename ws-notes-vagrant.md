#create 3 VMs all connected, ready for kubernetes installation
cd /Users/wassimsoualhi/work/Trainings/udemy_cka/certified-kubernetes-administrator-course
vagrant status
vagrant global-status
vagrant up
vagrant destroy -f
vagrant ssh <name of the nodes>
vagrant box list

#find config of vagrant vm
vagrant ssh-config 583bc10

#cheat sheet
https://gist.github.com/wpscholar/a49594e2e2b918f4d0c4