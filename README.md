# k0s-multicloud
**Up and Running k0s across Multicloud**

**Setup of Control Plane on GCP**<br>
Once you have created your virtual machine on GCP (GCE - in my example I have created a 2 x CPU, 4GB and 50GB disk instance with Ubuntu 20.04 LTS) ssh to the server
to run the following installation command<br>
#sudo curl -sSLf k0s.sh | sudo sh

**Setup of Workload Node1 on iMac**</br>
Pre-requisits: Please ensure that you have already installed Multipass on your iMac (Ref:  https://medium.com/platformer-blog/up-and-running-k3s-with-multipass-on-imac-or-macbook-pro-bee069247cc0) <br>
Open a terminal and type in the following command to create a virtual machine using Multipass<br>

#multipass launch --name k0s-workload-node1 --cpus 2 --mem 2GB --disk 10GB focal

Update and upgrade if required<br>
#sudo curl -sSLf k0s.sh | sudo sh

**Setup of Workload Node2 on DigitalOcean**<br>
ssh to the virtual machine you have just created <br>
#sudo curl -sSLf k0s.sh | sudo sh

**Setup of Workload Node2 on GCP**<br>
ssh to the virtual machine you have just created <br>
#sudo curl -sSLf k0s.sh | sudo sh
