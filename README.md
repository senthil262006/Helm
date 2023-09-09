# Helm

During Micro structure Aechetecure based applicatios deployments on Kubernetics

We have to create below objects 

One pod 
One deployments 
One replicaset
One services

Lifecycle mangement is too complex



gcloud compute instances create controlplane --project=moonlit-web-398217 --zone=us-central1-a --machine-type=e2-standard-4 --network-interface=network-tier=PREMIUM,stack-type=IPV4_ONLY,subnet=default --maintenance-policy=MIGRATE --provisioning-model=STANDARD --service-account=396745546933-compute@developer.gserviceaccount.com --scopes=https://www.googleapis.com/auth/devstorage.read_only,https://www.googleapis.com/auth/logging.write,https://www.googleapis.com/auth/monitoring.write,https://www.googleapis.com/auth/servicecontrol,https://www.googleapis.com/auth/service.management.readonly,https://www.googleapis.com/auth/trace.append --create-disk=auto-delete=yes,boot=yes,device-name=instance-1,image=projects/centos-cloud/global/images/centos-stream-8-v20230809,mode=rw,size=20,type=projects/moonlit-web-398217/zones/us-central1-a/diskTypes/pd-balanced --no-shielded-secure-boot --shielded-vtpm --shielded-integrity-monitoring --labels=goog-ec-src=vm_add-gcloud --reservation-affinity=any

gcloud compute instances create worker1 --project=moonlit-web-398217 --zone=us-central1-a --machine-type=e2-standard-4 --network-interface=network-tier=PREMIUM,stack-type=IPV4_ONLY,subnet=default --maintenance-policy=MIGRATE --provisioning-model=STANDARD --service-account=396745546933-compute@developer.gserviceaccount.com --scopes=https://www.googleapis.com/auth/devstorage.read_only,https://www.googleapis.com/auth/logging.write,https://www.googleapis.com/auth/monitoring.write,https://www.googleapis.com/auth/servicecontrol,https://www.googleapis.com/auth/service.management.readonly,https://www.googleapis.com/auth/trace.append --create-disk=auto-delete=yes,boot=yes,device-name=instance-1,image=projects/centos-cloud/global/images/centos-stream-8-v20230809,mode=rw,size=20,type=projects/moonlit-web-398217/zones/us-central1-a/diskTypes/pd-balanced --no-shielded-secure-boot --shielded-vtpm --shielded-integrity-monitoring --labels=goog-ec-src=vm_add-gcloud --reservation-affinity=any

gcloud compute instances create worker2 --project=moonlit-web-398217 --zone=us-central1-a --machine-type=e2-standard-4 --network-interface=network-tier=PREMIUM,stack-type=IPV4_ONLY,subnet=default --maintenance-policy=MIGRATE --provisioning-model=STANDARD --service-account=396745546933-compute@developer.gserviceaccount.com --scopes=https://www.googleapis.com/auth/devstorage.read_only,https://www.googleapis.com/auth/logging.write,https://www.googleapis.com/auth/monitoring.write,https://www.googleapis.com/auth/servicecontrol,https://www.googleapis.com/auth/service.management.readonly,https://www.googleapis.com/auth/trace.append --create-disk=auto-delete=yes,boot=yes,device-name=instance-1,image=projects/centos-cloud/global/images/centos-stream-8-v20230809,mode=rw,size=20,type=projects/moonlit-web-398217/zones/us-central1-a/diskTypes/pd-balanced --no-shielded-secure-boot --shielded-vtpm --shielded-integrity-monitoring --labels=goog-ec-src=vm_add-gcloud --reservation-affinity=any




modprobe bridge
 echo "net.bridge.bridge-nf-call-iptables = 1" >> /etc/sysctl.conf
 echo "net.ipv4.ip_forward = 1" >>/etc/sysctl.conf
 modprobe br_netfilter
 sysctl -p /etc/sysctl.conf
 
 sudo sed -i '/swap/d' /etc/fstab
sudo swapoff -a


#To see the stack trace of this error execute with --v=5 or higher
systemctl disable  firewalld
systemctl stop  firewalld


export VERSION=1.25
export OS=CentOS_8
curl -L -o /etc/yum.repos.d/devel:kubic:libcontainers:stable.repo https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/$OS/devel:kubic:libcontainers:stable.repo
curl -L -o /etc/yum.repos.d/devel:kubic:libcontainers:stable:cri-o:$VERSION.repo https://download.opensuse.org/repositories/devel:kubic:libcontainers:stable:cri-o:$VERSION/$OS/devel:kubic:libcontainers:stable:cri-o:$VERSION.repo
yum install -y crio
systemctl enable crio
systemctl start crio

cat <<EOF > /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
EOF

dnf --showduplicates list  kubeadm

#Install Kubernetes (kubeadm, kubelet and kubectl)
dnf install -y kubeadm-1.26.6-0 kubelet-1.26.6-0 kubectl-1.26.6-0

systemctl enable kubelet.service


sudo firewall-cmd --permanent --add-port=6443/tcp
sudo firewall-cmd --permanent --add-port=2379-2380/tcp
sudo firewall-cmd --permanent --add-port=10250/tcp
sudo firewall-cmd --permanent --add-port=10251/tcp
sudo firewall-cmd --permanent --add-port=10252/tcp
sudo firewall-cmd --permanent --add-port=10255/tcp
sudo firewall-cmd --reload

kubeadm init  --pod-network=10.67.0.0/24

export KUBECONFIG=/etc/kubernetes/admin.conf

kubectl apply -f https://github.com/flannel-io/flannel/releases/latest/download/kube-flannel.yml

kubeadm token generate
hp9b0k.1g9tqz8vkf78ucwf

kubeadm token create hp9b0k.1g9tqz8vkf78ucwf --print-join-command
