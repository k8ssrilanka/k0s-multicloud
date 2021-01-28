# k0s-multicloud
## Up and Running k0s across Multicloud

### Setup of Control Plane on DigitalOcen
Once you have created your virtual machine on DO (Droplets - in my example I have created a 2 x CPU, 4GB and 80GB disk instance with Ubuntu 18.04 LTS) ssh to the server
to run the following installation command<br>
Update and upgrade if required AND reboot<br>
```
#sudo apt update && sudo apt upgrade -y && sudo reboot
```
After the reboot run the following command to download k0s binary and install it<br>
```
#sudo curl -sSLf k0s.sh | sudo sh
```
Run k0s as a server in the background, in a production envrionment you would setup with systemd service<br>
```
#sudo sudo k0s server </dev/null &>/dev/null &
```
Take a copy of the kubernetes configuration to run locally or on your PC (this example shows that I am running it locally on the control plane node)<br>
First install kubectl<br>
```
#sudo snap install kubectl --classic
```
Copy the config file and setup envrionment variable<br>
```
#sudo cp /var/lib/k0s/pki/admin.conf admin.conf
#export KUBECONFIG=admin.conf
```
Test to make sure you can see the cluster nodes, at this stage you should not have any cluster nodes. However it should connect to the control plane to provide you an answer "no resources found"<br>
```
#kubectl get nodes -o wide
```
Create the token for workload nodes to connect<br>
```
#k0s token create --role=worker > workload-token.txt
```

### Setup of Workload Dev on iMac
Pre-requisits: Please ensure that you have already installed [Multipass on your iMac](https://medium.com/platformer-blog/up-and-running-k3s-with-multipass-on-imac-or-macbook-pro-bee069247cc0) <br>
Open a terminal and type in the following command to create a virtual machine using Multipass<br>
```
#multipass launch --name k0s-dev-node1 --cpus 2 --mem 2GB --disk 10GB focal
#multipass shell k0s-dev-node1
```
Update and upgrade if required AND reboot<br>
```
#sudo apt update && sudo apt upgrade -y && sudo reboot
```
After the reboot run the following command to download k0s binary and install it<br>
```
#sudo curl -sSLf k0s.sh | sudo sh
```
Connect to the control plane with the token created<br>
```
#sudo k0s worker --token-file workload-token.txt
```
### Setup of Workload Test on GCP
ssh to the virtual machine you have just created <br>
Update and upgrade if required AND reboot<br>
```
#sudo apt update && sudo apt upgrade -y && sudo reboot
#sudo curl -sSLf k0s.sh | sudo sh
```
Connect to the control plane with the token created<br>
```
#sudo k0s worker --token-file workload-token.txt
```
### Setup of Workload Prodution on GCP
ssh to the virtual machine you have just created <br>
Update and upgrade if required AND reboot<br>
```
#sudo apt update && sudo apt upgrade -y && sudo reboot
#sudo curl -sSLf k0s.sh | sudo sh
```
Connect to the control plane with the token created<br>
```
#sudo k0s worker --token-file workload-token.txt
```

### Webinar questions and Answers

[Slides used for the presentation](https://docs.google.com/presentation/d/1ONKz-bXvQuQaL3Zk8PxtfYXtkPPCxG30q3f79WTT57I/edit?usp=sharing)

Q1. If we distribute our applications across multiple cloud providers wont we have latency issues when the service is exposed? <br>
A1. Short answer is YES. However there are situations where you may need go distribute the application and have geo-based loadbalancing where customers get responses from the closest cluster where the pods are running. The examples I demoed today are more focused on running dev on-premise, test on a low cost cloud and production is a different cloud. 

Q2. How do we overcome the issue with GCP control plane?
A2. I have not figured that out yet, once I have will provide a reply here. 

### Other References
[k0s Project Site](https://k0sproject.io/)<br>
[Container Networking](https://iximiuz.com/en/posts/container-networking-is-simple/)
