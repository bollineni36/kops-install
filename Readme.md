General Architecture of K8s Cluster:

![Image description](https://miro.medium.com/max/1190/0*sGRplim9zUwPPeXB.png)

Intended architecture for LAMP stack on K8s Cluster with minimal nodes:
The underlying cloud can be anything Azure, AWS or GCP; for this example we have given AWS as a cloud provider.

![Image description](http://docs.heptio.com/_images/lamp-001.png)

Implementation steps using rhel7:
sudo su

# Install kops

curl -LO https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64

chmod +x kops-linux-amd64

 sudo mv kops-linux-amd64 /usr/local/bin/kops
 ln -s /usr/local/bin/kops /usr/bin/kops

# In GCP created "Cloud DNS"

 useast
 Registrar Setup
DNS nameuseast1.dev.example.com.TypePublic
Record sets
 
DNS name	Type	TTL (seconds)	Data	
useast1.dev.example.com.	NS	21600	
ns-cloud-c1.googledomains.com.
ns-cloud-c2.googledomains.com.
ns-cloud-c3.googledomains.com.
ns-cloud-c4.googledomains.com.
useast1.dev.example.com.	SOA	21600	
ns-cloud-c1.googledomains.com. cloud-dns-hostmaster.google.com. 1 21600 3600 259200 300

# Test in the node if you are able to resolve the domain

 dig useast1.dev.example.com

  yum install bind-utils - to install dig if missing


# INstall kubectl
[root@node2 ~]# curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 44.5M  100 44.5M    0     0   116M      0 --:--:-- --:--:-- --:--:--  116M
[root@node2 ~]# chmod +x ./kubectl
[root@node2 ~]# sudo mv ./kubectl /usr/local/bin/kubectl
[root@node2 ~]# ln -s /usr/local/bin/kubectl /usr/bin/kubectl


[root@node2 ~]# kubectl version
Client Version: version.Info{Major:"1", Minor:"16", GitVersion:"v1.16.3", GitCommit:"b3cbbae08ec52a7fc73d334838e18d17e8512749", GitTreeState:"clean", BuildDate:"2019-11-13T11:23:11Z", GoVersion:"go1.12.12", Compil
er:"gc", Platform:"linux/amd64"}
The connection to the server localhost:8080 was refused - did you specify the right host or port?
[root@node2 ~]# 

# Install gcloud tools

https://cloud.google.com/sdk/docs/downloads-yum


# Made astorage bucket in gcp  and made it public using this link
  https://cloud.google.com/storage/docs/access-control/making-data-public

 and set the env variable

[root@node2 ~]# gsutil mb gs://kubernetes-clusters-rparuchuri
Creating gs://kubernetes-clusters-rparuchuri/...
[root@node2 ~]#  export KOPS_STATE_STORE=gs://kubernetes-clusters-rparuchuri


Precisely following instructions from here now:

https://www.cloudtechnologyexperts.com/kubernetes-google-cloud-kops/

