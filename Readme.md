General Architecture of K8s Cluster:

![Image description](https://miro.medium.com/max/1190/0*sGRplim9zUwPPeXB.png)

Intended architecture for LAMP stack on K8s Cluster with minimal nodes:
The underlying cloud can be anything Azure, AWS or GCP; for this example we have given AWS as a cloud provider.

![Image description](http://docs.heptio.com/_images/lamp-001.png)

Implementation steps using rhel7:
sudo su

curl -LO https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64

chmod +x kops-linux-amd64

 sudo mv kops-linux-amd64 /usr/local/bin/kops

 *In GCP created "Cloud DNS"*

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

--> Test in the node if you are able to resolve the domain

 dig useast1.dev.example.com

  # yum install bind-utils - to install dig if missing

