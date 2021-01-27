# k0s-multicloud
**Up and Running k0s across Multicloud**

**Setup of Control Plane on DigitalOcen**<br>
Once you have created your virtual machine on DO (Droplets - in my example I have created a 2 x CPU, 4GB and 80GB disk instance with Ubuntu 18.04 LTS) ssh to the server
to run the following installation command<br>
Update and upgrade if required AND reboot<br>
#sudo apt update && sudo apt upgrade -y && sudo reboot<br>

After the reboot run the following command to download k0s binary and install it<br>
#sudo curl -sSLf k0s.sh | sudo sh

**Setup of Workload Dev on iMac**</br>
Pre-requisits: Please ensure that you have already installed Multipass on your iMac (Ref:  https://medium.com/platformer-blog/up-and-running-k3s-with-multipass-on-imac-or-macbook-pro-bee069247cc0) <br>
Open a terminal and type in the following command to create a virtual machine using Multipass<br>

#multipass launch --name k0s-workload-node1 --cpus 2 --mem 2GB --disk 10GB focal

Update and upgrade if required AND reboot<br>
#sudo apt update && sudo apt upgrade -y && sudo reboot<br>

After the reboot run the following command to download k0s binary and install it<br>
#sudo curl -sSLf k0s.sh | sudo sh

**Setup of Workload Test on GCP**<br>
ssh to the virtual machine you have just created <br>
Update and upgrade if required AND reboot<br>
#sudo apt update && sudo apt upgrade -y && sudo reboot<br>
#sudo curl -sSLf k0s.sh | sudo sh

**Setup of Workload Prodution on GCP**<br>
ssh to the virtual machine you have just created <br>
Update and upgrade if required AND reboot<br>
#sudo apt update && sudo apt upgrade -y && sudo reboot
#sudo curl -sSLf k0s.sh | sudo sh
